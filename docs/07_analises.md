# 7. Análises

As análises foram estruturadas para permitir avaliação de desempenho financeiro sob diferentes perspectivas, apoiando a tomada de decisão.

---

## 7.1 Análise Horizontal (AH)

Avalia a variação dos indicadores ao longo do tempo.

### Objetivo
- Identificar crescimento ou retração dos resultados
- Detectar tendências de desempenho

### Abordagem
- Comparação com períodos anteriores (Year over Year)
- Cálculo de variação percentual (% Δ)

---

## 7.2 Análise Vertical (AV)

Analisa a representatividade de cada conta em relação ao total.

### Objetivo
- Entender a composição da DRE
- Avaliar peso de custos e despesas sobre a receita

### Abordagem
- Percentual de cada linha em relação à Receita Bruta

---

## 7.3 Evolução Histórica

Permite visualizar o comportamento dos indicadores ao longo do tempo.

### Objetivo
- Identificar padrões de crescimento
- Avaliar consistência dos resultados

### Abordagem
- Análise temporal com base na dimensão calendário (`dCalendario`)
- Suporte a comparações anuais e mensais

---

## 7.4 Implementação Técnica

As análises foram implementadas em DAX, utilizando funções de inteligência temporal e contexto de filtro:

- `SAMEPERIODLASTYEAR`
- `PREVIOUSYEAR`
- `CALCULATE` e manipulação de contexto

[Explorar implementações DAX](../scripts/dax/README.md)

---

## Rastreabilidade

As análises estão diretamente conectadas a:

- Modelagem de dados → seção 5  
- Indicadores (KPIs) → seção 6  
- Implementação técnica → scripts DAX  

Garantindo consistência entre estrutura de dados e interpretação analítica.
