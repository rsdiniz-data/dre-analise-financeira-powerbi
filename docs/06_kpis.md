# 6. Indicadores (KPIs)

## 6.1 Principais Métricas

Os principais indicadores financeiros foram estruturados com base na DRE:

- Receita Bruta
- Custos
- Despesas
- EBITDA
- EBIT
- Lucro Líquido

---

## 6.2 Lógica de Cálculo

Os indicadores foram construídos em DAX, utilizando a estrutura da modelagem dimensional.

A apuração segue a classificação contábil definida na dimensão `dPlanoConta`, garantindo consistência entre:

- Estrutura da DRE
- Regras de negócio
- Cálculo dos indicadores

---

## 6.3 Exemplo de Implementação

A **Receita Bruta** é calculada a partir das contas classificadas como receita operacional.

Essa classificação é definida pelo campo `CodDRE`, onde:

- `"3.01"` representa contas de Receita

### Regra aplicada:

- Filtrar contas com `CodDRE = "3.01"`
- Agregar os valores na tabela fato (`ftResultado`)

Essa abordagem garante que o indicador respeite a estrutura contábil da DRE.

---

## 6.4 Implementação Técnica

Os cálculos foram implementados em DAX, organizados por categoria:

- KPIs principais
- Análises (AH, AV, YoY)
- Simulações (What-If)
- Medidas auxiliares

[Explorar documentação DAX](../scripts/dax/README.md)

---

## Rastreabilidade

Os indicadores estão diretamente conectados a:

- Modelagem de dados → seção 5  
- Pipeline de dados → seção 4  
- Implementação técnica → scripts DAX  

Essa estrutura permite validação completa do fluxo:

**dado bruto → transformação → modelagem → cálculo do KPI**
