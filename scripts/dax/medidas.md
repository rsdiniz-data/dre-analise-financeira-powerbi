-- =========================================================
-- PROJETO: DRE Automatizada
-- ARQUIVO: medidas.md
-- =========================================================

-- =========================================================
-- BASE
-- Referência: docs/04_pipeline_dados.md | Seção 4
-- =========================================================

R$ | Total Resultado =
SUM(ftResultado[Valor])

------------------------------------------------------------

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

-- =========================================================
-- KPIs PRINCIPAIS
-- Referência: docs/06_kpis.md | Seção 6.1
-- =========================================================

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

-- =========================================================
-- ANÁLISES (AH / AV)
-- Referência: docs/07_analises.md
-- =========================================================

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

-- =========================================================
-- AUXILIARES
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
-- YOY (VALOR)
-- Referência: docs/07_analises.md
-- =========================================================

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

-- =========================================================
-- YOY (%)
-- =========================================================

% Δ | Receita Bruta YoY =
DIVIDE([R$ | Receita Bruta YoY], CALCULATE([R$ | Receita Bruta], PREVIOUSYEAR(dCalendario[Data])))

% Δ | Custos YoY =
DIVIDE([R$ | Custos YoY], CALCULATE([R$ | Custos], PREVIOUSYEAR(dCalendario[Data])))

% Δ | EBITDA YoY =
DIVIDE([R$ | EBITDA YoY], CALCULATE([R$ | EBITDA], PREVIOUSYEAR(dCalendario[Data])))

% Δ | Lucro Liquido YoY =
DIVIDE([R$ | Lucro Liquido YoY], CALCULATE([R$ | Lucro Liquido], PREVIOUSYEAR(dCalendario[Data])))

-- =========================================================
-- SIMULAÇÕES (WHAT-IF)
-- Referência: docs/08_simulacoes.md
-- =========================================================

SIM | Receita WIF =
[R$ | Receita Bruta] * (1 + [WIFReceita Valor])

SIM | Custo WIF =
[R$ | Custos] * (1 + [WIFCusto Valor])

SIM | Despesa WIF =
[R$ | Despesas] * (1 + [WIFDespesas Valor])

SIM | Margem WIF =
[SIM | Receita WIF] + [SIM | Custo WIF]

SIM | EBIT WIF =
[SIM | Margem WIF] + [SIM | Despesa WIF]

-- =========================================================
-- IMPACTO DAS SIMULAÇÕES
-- =========================================================

Δ | Impacto Receita =
[SIM | Receita WIF] - [R$ | Receita Bruta]

Δ | Impacto Custo =
[SIM | Custo WIF] - [R$ | Custos]

Δ | Impacto Despesa =
[SIM | Despesa WIF] - [R$ | Despesas]

Δ | Impacto Margem =
[SIM | Margem WIF] - [R$ | Margem Bruta]

Δ | Impacto EBIT =
[SIM | EBIT WIF] - [R$ | EBIT]
