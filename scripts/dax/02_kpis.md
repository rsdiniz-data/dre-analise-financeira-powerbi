# 🔹 KPIs PRINCIPAIS

**Referência:** docs/06_kpis.md | Seção 6.1

## R$ | Receita Bruta
```dax
R$ | Receita Bruta =
CALCULATE([R$ | Total Resultado], dPlanoConta[CodDRE] = "3.01")

R$ | Custos =
CALCULATE([R$ | Total Resultado], dPlanoConta[CodDRE] = "3.02")

R$ | Margem Bruta =
CALCULATE([R$ | DRE], dPlanoConta[CodDRE] = "3.03")

R$ | Despesas =
CALCULATE([R$ | Total Resultado], dPlanoConta[CodDRE] = "3.04")

R$ | EBIT =
CALCULATE([R$ | DRE], dPlanoConta[CodDRE] = "3.05")

R$ | EBITDA =
CALCULATE([R$ | DRE], dPlanoConta[ID Conta] = "3.07")

R$ | Lucro Liquido =
CALCULATE([R$ | DRE], dPlanoConta[CodDRE] = "3.11")

R$ | DRE =
VAR vEscopo = SELECTEDVALUE(dPlanoConta[CodDRE])
VAR vResultado =
CALCULATE(
    [R$ | Total Resultado],
    FILTER(
        ALL(dPlanoConta),
        dPlanoConta[ID Conta] < vEscopo
    )
)
RETURN
SWITCH(
    TRUE(),
    ISINSCOPE(dPlanoConta[N2]) && SELECTEDVALUE(dPlanoConta[N2]) = BLANK(), BLANK(),
    SELECTEDVALUE(dPlanoConta[Lançamento]) = 1 || SELECTEDVALUE(dPlanoConta[Calculado]) = 0, [R$ | Total Resultado],
    SELECTEDVALUE(dPlanoConta[Calculado]) = 1 && NOT(ISINSCOPE(dPlanoConta[N2])) && NOT(ISINSCOPE(dPlanoConta[N3])), vResultado,
    BLANK()
)
```
