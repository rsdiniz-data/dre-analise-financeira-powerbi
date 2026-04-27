# 🔹 YoY (Valor)

**Referência:** docs/07_analises.md | Seção 7.3

```dax
R$ | Receita Bruta YoY =
VAR vPY = CALCULATE([R$ | Receita Bruta], PREVIOUSYEAR(dCalendario[Data]))
RETURN
IF(
    HASONEVALUE(dCalendario[Ano]) && NOT ISBLANK(vPY),
    [R$ | Receita Bruta] - vPY
)

R$ | Custos YoY =
VAR vPY = CALCULATE([R$ | Custos], PREVIOUSYEAR(dCalendario[Data]))
RETURN
IF(
    HASONEVALUE(dCalendario[Ano]) && NOT ISBLANK(vPY),
    [R$ | Custos] - vPY
)

R$ | EBITDA YoY =
VAR vPY = CALCULATE([R$ | EBITDA], PREVIOUSYEAR(dCalendario[Data]))
RETURN
IF(
    HASONEVALUE(dCalendario[Ano]) && NOT ISBLANK(vPY),
    [R$ | EBITDA] - vPY
)

R$ | Lucro Liquido YoY =
VAR vPY = CALCULATE([R$ | Lucro Liquido], PREVIOUSYEAR(dCalendario[Data]))
RETURN
IF(
    HASONEVALUE(dCalendario[Ano]) && NOT ISBLANK(vPY),
    [R$ | Lucro Liquido] - vPY
)
```
