# 🔹SIMULAÇÕES (WHAT-IF)

**Referência:** docs/08_simulacoes.md | Seção 8.4

```dax
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
```
# 🔹IMPACTO DAS SIMULAÇÕES

**Referência:** docs/08_simulacoes.md | Seção 8.4

```dax
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
```
