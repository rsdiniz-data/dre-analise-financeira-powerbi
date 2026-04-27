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
```
