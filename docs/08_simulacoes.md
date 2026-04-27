# 8. Simulações

Foi implementado um modelo de simulação (What-If) para análise de cenários, permitindo avaliar o impacto de variações nos principais componentes da DRE.

---

## 8.1 Parâmetros de Simulação

O modelo permite simular variações nos seguintes indicadores:

- Receita
- Custos
- Despesas

Os parâmetros são controlados dinamicamente pelo usuário no dashboard.

---

## 8.2 Objetivo

- Avaliar impactos de decisões antes da execução
- Apoiar planejamento financeiro
- Simular cenários otimistas e pessimistas

---

## 8.3 Abordagem

As simulações foram implementadas utilizando parâmetros What-If no Power BI, com aplicação direta sobre os valores base:

- Ajuste percentual aplicado sobre os indicadores originais
- Recalculo automático de margens e resultado operacional

---

## 8.4 Impactos Calculados

A partir das simulações, são recalculados:

- Receita simulada
- Custos simulados
- Despesas simuladas
- Margem
- EBIT

Além disso, são apresentados os impactos absolutos:

- Δ Receita
- Δ Custos
- Δ Despesas
- Δ Margem
- Δ EBIT

---

## 8.5 Implementação Técnica

As simulações foram implementadas em DAX, utilizando medidas específicas para cenário:

- 📊 Medidas simuladas (WIF)
- 📈 Medidas de impacto (Δ)
- 🔧 Parâmetros dinâmicos

👉 [Explorar implementações DAX](../scripts/dax/README.md)

---

## 🔗 Rastreabilidade

As simulações estão conectadas a:

- Indicadores base → seção 6  
- Análises → seção 7  
- Implementação técnica → scripts DAX  

Essa estrutura permite comparar diretamente:

**cenário atual vs cenário simulado**
