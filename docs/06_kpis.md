# 6. Indicadores (KPIs)

## 6.1 Principais Métricas

- Receita Bruta
- Custos
- Despesas
- EBITDA
- EBIT
- Lucro Líquido

## 6.2 Cálculo

Os indicadores foram construídos utilizando DAX, com base na estrutura da DRE.

Scripts relacionados:
- [Ver medidas DAX](../scripts/dax/medidas.md)

## 6.3 Exemplo de Implementação

A Receita Bruta é calculada a partir da soma dos valores financeiros classificados como receita no plano de contas.

Essa classificação é feita através do campo `CodDRE`, onde:

- "3.01" representa contas de Receita

Dessa forma, o cálculo consiste em:

- Filtrar apenas contas com `CodDRE = "3.01"`
- Somar os valores correspondentes na tabela fato

A implementação pode ser vista em:

- [Ver medidas DAX](../scripts/dax/medidas.md)
