# 5. Modelagem de Dados

A modelagem foi estruturada seguindo o padrão **Star Schema**, com separação entre tabela fato e dimensões, permitindo análises eficientes e escaláveis.

---

## 5.1 Estrutura do Modelo

O modelo é composto por:

- **Tabela Fato**
  - `ftResultado` → armazena valores financeiros por conta e data

- **Dimensões**
  - `dPlanoConta` → estrutura hierárquica da DRE (N1, N2, N3)
  - `dCalendario` → suporte a análises temporais (Ano, Mês)

---

## 5.2 Transformações Aplicadas

Durante a preparação dos dados, foram aplicadas as seguintes transformações:

- **Unpivot de colunas**
  - Conversão de colunas de anos para formato linha (modelo analítico)

- **Hierarquia contábil**
  - Construção dos níveis N1, N2 e N3 com base no código da conta

- **Classificação de contas**
  - Identificação de natureza financeira (Receita vs Custos/Despesas)

---

## 5.3 Regras de Negócio

- Exclusão de contas sintéticas
- Consideração apenas de contas analíticas (`Lançamento = 1`)
- Padronização de tipos de dados
- Enriquecimento da tabela fato via relacionamento com dimensão

---

## 5.4 Implementação Técnica

As transformações foram implementadas utilizando Power Query (M), organizadas por responsabilidade:

- [Dimensão Plano de Contas](.scripts/powerquery/03_dim_plano_conta.md)
- [Tabela Fato (Resultado)](.scripts/powerquery/04_ft_resultado.md)
- [Dimensão Calendário](.scripts/powerquery/05_dim_calendario.md)

---

## 🔗 Rastreabilidade

A modelagem está diretamente conectada ao pipeline de dados (seção 4) e aos cálculos analíticos (seção 6), garantindo consistência entre:

- Estrutura dos dados
- Regras de negócio
- Implementação técnica





📄 Ver detalhes: [Explorar documentação Power Query](../scripts/powerquery/README.md)
