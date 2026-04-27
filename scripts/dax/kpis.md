```sql
-- =========================================================
-- PROJETO: DRE Automatizada
-- ARQUIVO: kpis.md
-- =========================================================

-- =========================================================
-- 🔹 KPIs PRINCIPAIS
-- Referência: docs/06_kpis.md
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
```
