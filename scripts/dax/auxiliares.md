```sql
-- =========================================================
-- PROJETO: DRE Automatizada
-- ARQUIVO: yoy_simulacoes.md
-- =========================================================

-- =========================================================
-- 🔹 AUXILIARES
-- Referência: docs/07_analises.md
-- =========================================================

AUX | Direção Indicador =
VAR vTipo = SELECTEDVALUE(dPlanoConta[TipoIndicador])
RETURN [% Δ | AH DRE] * vTipo

AUX | Filtro Selecionado =
VAR vAnoSelecionado = VALUES(dCalendario[Ano])
RETURN
"Filtro Aplicado: " &
CONCATENATEX(vAnoSelecionado, dCalendario[Ano], ", ")

AUX | Texto Título Rótulo =
"vs ano anterior"

-- =========================================================
-- 🔹 AUXILIARES (YoY)
-- Referência: docs/07_analises.md
-- =========================================================

"AUX | % R$ Δ | Custos YoY =
VAR vYoY = [R$ | Custos YoY]
VAR vNum = [AUX | R$ | Custos YoY]
VAR vPerc = FORMAT([% Δ | Custos YoY], ""▼ +0.0%; ▲ -0.0%;0%"")
RETURN
IF(
    ISBLANK(vYoY),
    ""--"",
    vPerc & "" | "" & vNum
)"
"AUX | % R$ Δ | EBITDA YoY =
VAR vYoY = [R$ | EBITDA YoY]
VAR vNum = [AUX | R$ | EBITDA YoY]
VAR vPerc = FORMAT([% Δ | EBITDA YoY], ""▲ +0.0%; ▼ -0.0%;0%"")
RETURN
IF(
    ISBLANK(vYoY),
    ""--"",
    vPerc & "" | "" & vNum
)"
"AUX | % R$ Δ | Lucro Liquido YoY =
VAR vYoY = [R$ | Lucro Liquido YoY]
VAR vNum = [AUX | R$ | Lucro Liquido YoY]
VAR vPerc = FORMAT([% Δ | Lucro Liquido YoY], ""▲ +0.0%; ▼ -0.0%;0%"")
RETURN
IF(
    ISBLANK(vYoY),
    ""--"",
    vPerc & "" | "" & vNum
)"
"AUX | % R$ Δ | Receita Bruta YoY =
VAR vYoY = [R$ | Receita Bruta YoY]
VAR vNum = [AUX | R$ | Receita Bruta YoY]
VAR vPerc = FORMAT([% Δ | Receita Bruta YoY], ""▲ +0.0%; ▼ -0.0%;0%"")
RETURN
IF(
    ISBLANK(vYoY),
    ""--"",
    vPerc & "" | "" & vNum
)"
"AUX | R$ | Custos YoY =
VAR vValor = [R$ | Custos YoY]
VAR vAbs = ABS(vValor)
RETURN
SWITCH(
    TRUE(),
    
    vAbs >= 1000000000,
        FORMAT(vValor / 1000000000, ""0.00;0.00;0"") & "" Bi"",
        
    vAbs >= 1000000,
        FORMAT(vValor / 1000000, ""0.00;0.00;0"") & "" Mi"",
        
    vAbs >= 1000,
        FORMAT(vValor / 1000, ""0.00;0.00;0"") & "" Mil"",
        
    FORMAT(vValor, ""+0;-0;0"")
)"
"AUX | R$ | EBITDA YoY =
VAR vValor = [R$ | EBITDA YoY]
VAR vAbs = ABS(vValor)
RETURN
SWITCH(
    TRUE(),
    
    vAbs >= 1000000000,
        FORMAT(vValor / 1000000000, ""0.00;0.00;0"") & "" Bi"",
        
    vAbs >= 1000000,
        FORMAT(vValor / 1000000, ""0.00;0.00;0"") & "" Mi"",
        
    vAbs >= 1000,
        FORMAT(vValor / 1000, ""0.00;0.00;0"") & "" Mil"",
        
    FORMAT(vValor, ""+0;-0;0"")
)"
"AUX | R$ | Lucro Liquido YoY =
VAR vValor = [R$ | Lucro Liquido YoY]
VAR vAbs = ABS(vValor)
RETURN
SWITCH(
    TRUE(),
    
    vAbs >= 1000000000,
        FORMAT(vValor / 1000000000, ""0.00;0.00;0"") & "" Bi"",
        
    vAbs >= 1000000,
        FORMAT(vValor / 1000000, ""0.00;0.00;0"") & "" Mi"",
        
    vAbs >= 1000,
        FORMAT(vValor / 1000, ""0.00;0.00;0"") & "" Mil"",
        
    FORMAT(vValor, ""+0;-0;0"")
)"
"AUX | R$ | Receita Bruta YoY =
VAR vValor = [R$ | Receita Bruta YoY]
VAR vAbs = ABS(vValor)
RETURN
SWITCH(
    TRUE(),
    
    vAbs >= 1000000000,
        FORMAT(vValor / 1000000000, ""0.00;0.00;0"") & "" Bi"",
        
    vAbs >= 1000000,
        FORMAT(vValor / 1000000, ""0.00;0.00;0"") & "" Mi"",
        
    vAbs >= 1000,
        FORMAT(vValor / 1000, ""0.00;0.00;0"") & "" Mil"",
        
    FORMAT(vValor, ""+0;-0;0"")
)"
```
