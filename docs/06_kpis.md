# 6. Indicadores (KPIs)

## 🎯 Objetivo

Estruturar indicadores financeiros para análise da performance econômica da empresa, utilizando a modelagem dimensional e as regras contábeis da DRE.

Os KPIs foram desenvolvidos para apoiar análises gerenciais, comparações históricas e acompanhamento da evolução dos resultados financeiros.

---

## 📊 Principais Indicadores

Indicadores implementados no modelo:

- Receita Bruta
- Custos
- Despesas
- EBITDA
- EBIT
- Lucro Líquido
- Margem Bruta
- Margem EBITDA

---

## ⚙️ Estrutura de Cálculo

As métricas foram desenvolvidas em DAX utilizando:

- Tabela fato `ftResultado`
- Dimensão `dPlanoConta`
- Hierarquia da DRE (`N1`, `N2`, `N3`)
- Classificação contábil (`CodDRE` e `TipoIndicador`)

Essa abordagem garante consistência entre:

- Regras de negócio
- Estrutura contábil
- Indicadores financeiros

---

## 📈 Análises Implementadas

Além dos KPIs principais, o modelo suporta:

- YoY (Year over Year)
- AH (Análise Horizontal)
- AV (Análise Vertical)
- Comparações temporais
- Indicadores percentuais

---

## 💻 Implementação Técnica

As medidas DAX foram organizadas por responsabilidade:

- [KPIs principais](../scripts/dax/02_kpis.md)
- [Análises financeiras](../scripts/dax/03_analises.md)
- [Simulações What-If](../scripts/dax/06_simulacoes.md)
- [Medidas auxiliares](../scripts/dax/07_auxiliares.md)

📄 Ver visão completa:
👉 [Explorar documentação DAX](../scripts/dax/README.md)

---

## 📷 Indicadores no Dashboard

![KPIs Financeiros](../images/cartoes_executivos_indicadores_financeiros.png)

---

## 🔗 Rastreabilidade

Os indicadores estão conectados diretamente a:

- Desenvolvimento do projeto
- Modelagem dimensional
- Regras contábeis
- Scripts DAX

Fluxo completo:

`Fonte de Dados → Transformação → Modelagem → KPI`