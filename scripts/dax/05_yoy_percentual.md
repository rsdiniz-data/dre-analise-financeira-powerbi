# 🔹 YOY (%)

**Referência:** docs/07_analises.md

% Δ | Receita Bruta YoY =
DIVIDE([R$ | Receita Bruta YoY], CALCULATE([R$ | Receita Bruta], PREVIOUSYEAR(dCalendario[Data])))

% Δ | Custos YoY =
DIVIDE([R$ | Custos YoY], CALCULATE([R$ | Custos], PREVIOUSYEAR(dCalendario[Data])))

% Δ | EBITDA YoY =
DIVIDE([R$ | EBITDA YoY], CALCULATE([R$ | EBITDA], PREVIOUSYEAR(dCalendario[Data])))

% Δ | Lucro Liquido YoY =
DIVIDE([R$ | Lucro Liquido YoY], CALCULATE([R$ | Lucro Liquido], PREVIOUSYEAR(dCalendario[Data])))
```
