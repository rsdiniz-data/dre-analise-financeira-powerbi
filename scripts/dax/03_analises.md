# 🔹 Análises (AH / AV)

**Referência:** docs/07_analises.md | Seção 7.1 e 7.2

```dax
% Δ | AH DRE =
VAR vTipo = SELECTEDVALUE(dPlanoConta[TipoIndicador])
VAR vPY = CALCULATE([R$ | DRE], SAMEPERIODLASTYEAR(dCalendario[Data]))
RETURN
IF(
    vTipo = -1,
    DIVIDE([R$ | DRE] - vPY, vPY),
    DIVIDE([R$ | DRE] - vPY, ABS(vPY))
)

% Δ | AV DRE =
VAR ResultadoFixo =
CALCULATE([R$ | DRE], ALL(dPlanoConta), dPlanoConta[CodDRE] = "3.01")
RETURN
DIVIDE([R$ | DRE], ResultadoFixo)
```
