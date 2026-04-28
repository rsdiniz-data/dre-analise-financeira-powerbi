# 5. Dicionário de Dados
## 5.1 Tabela `dPlanoConta`
## Descrição

Dimensão responsável pela **hierarquia do plano de contas da DRE**, permitindo análises por nível (`N1`, `N2`, `N3`) e suportando a construção dos indicadores financeiros.

**Script relacionado:** [Ver transformação no Power Query](../scripts/powerquery/03_dim_plano_conta.md)

## Estrutura

| Coluna          | Tipo    | Descrição                                             | Relacionamentos                |
|-----------------|---------|-------------------------------------------------------|--------------------------------|
| `ID Conta`      | Texto   | Identificador único da conta contábil                 | 1:N → `ftResultado[ID Conta]`  |
| `Descrição`     | Texto   | Nome da conta                                        | —                              |
| `Lançamento`    | Inteiro | 1 = analítica / 0 = sintética                        | —                              |
| `N1`            | Texto   | Grupo principal (ex.: Receita, Custos)               | —                              |
| `N2`            | Texto   | Subgrupo contábil                                    | —                              |
| `N3`            | Texto   | Conta analítica                                      | —                              |
| `CodDRE`        | Texto   | Código da estrutura da DRE                           | —                              |
| `Calculado`     | Inteiro | Controle de agregações no modelo                     | —                              |
| `TipoIndicador` | Inteiro | Classificação do indicador (Receita, Custo, etc.)    | —                              |
## Observações
- Hierarquia baseada na estrutura do `ID Conta`
- Contas sintéticas (`Lançamento = 0`) são utilizadas apenas para agregação
- `TipoIndicador` auxilia no cálculo de variações (ex.: AH)

## 5.2 Tabela `ftResultado`
## Descrição

Tabela fato do modelo, contendo os **valores financeiros da DRE por conta e data**. Base para todos os cálculos e indicadores.

**Script relacionado:** [Ver transformação no Power Query](../scripts/powerquery/04_ft_resultado.md)

## Estrutura
Coluna       | Tipo     | Descrição                                   | Relacionamentos
-------------|----------|---------------------------------------------|-------------------------------
ID Conta     | Texto    | Conta contábil associada ao valor           | *:1 → dPlanoConta[ID Conta]
Data         | Data     | Data de referência (fechamento)             | *:1 → dCalendario[Data]
Valor        | Decimal  | Valor financeiro                            | —
## Observações
- Contém apenas contas analíticas (`Lançamento = 1`)
- Dados no formato long (unpivot)
- Base para KPIs e análises (YoY, AH, AV)

## 5.3 Tabela `dCalendario`
## Descrição

Dimensão de tempo utilizada para **análises temporais** e comparações entre períodos.

**Script relacionado:** [Ver transformação no Power Query](../scripts/powerquery//05_dim_calendario.md)

## Estrutura
Coluna	Tipo	Descrição	Relacionamentos
Data	Data	Data completa	1:* → ftResultado[Data]
Ano	Inteiro	Ano da data	—
Mes	Texto	Nome abreviado do mês	—
Mes_Num	Inteiro	Número do mês (ordenação)	—
## Observações
- Cobre todo o intervalo da `ftResultado`
- `Mes_Num` deve ser utilizado para ordenação do mês
- Pode ser expandida com novos atributos (trimestre, semana, etc.)

## 5.4 Estrutura do Modelo

Modelo dimensional no padrão Star Schema:

dPlanoConta (1:N) → ftResultado  
dCalendario (1:N) → ftResultado

## Considerações
- Separação clara entre fato e dimensões
- Estrutura escalável e de fácil manutenção
- Base sólida para construção de métricas em DAX
- Integração direta entre documentação e implementação (rastreabilidade)
