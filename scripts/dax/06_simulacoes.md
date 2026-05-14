# 🔹Simulações (What-If)

**Referência:** docs/07_metricas.md  
**Artigo Técnico:** docs/10_artigo_tecnico.md -> 7. Métricas e Indicadores (DAX) 

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
# 🔹Impacto das Simulações

**Referência:** docs/07_metricas.md  
**Artigo Técnico:** docs/10_artigo_tecnico.md -> 7. Métricas e Indicadores (DAX) 

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
