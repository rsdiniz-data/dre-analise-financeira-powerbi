# 🔹 Análises (AH / AV)

**Referência:** docs/07_metricas.md    
**Artigo Técnico:** docs/10_artigo_tecnico.md -> 7. Métricas e Indicadores (DAX) 

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
