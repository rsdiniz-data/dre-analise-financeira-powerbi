# 3. Arquitetura da Solução

## 🎯 Objetivo

Construir uma estrutura analítica organizada, rastreável e escalável para consolidação e análise da DRE.

A arquitetura foi desenvolvida utilizando modelagem dimensional (Star Schema), separando dados transacionais das estruturas analíticas para otimizar performance e facilitar manutenção.

---

## ⭐ Modelo Dimensional

### 📌 Tabela Fato

* `ftResultado`
  * Armazena os valores financeiros da DRE por conta e período

### 📌 Dimensões

* `dPlanoConta`
  * Estrutura hierárquica da DRE (N1, N2 e N3)

* `dCalendario`
  * Suporte para análises temporais e evolução histórica

---

## 🔗 Relacionamentos

`dPlanoConta (1) → (N) ftResultado`

`dCalendario (1) → (N) ftResultado`

---

## 📷 Modelo do Projeto

![Modelo Dimensional](../images/modelo_dimensional_star_schema_dre.png)

---

## 🔄 Fluxo da Solução

PDF / Excel → Power Query → Modelagem Dimensional → DAX → Power BI

---

## 🔗 Rastreabilidade

### ⚙️ Power Query

* [01_parametro.md](../scripts/powerquery/01_parametro.md)
* [02_extracao_pdf.md](../scripts/powerquery/02_extracao_pdf.md)
* [03_dim_plano_conta.md](../scripts/powerquery/03_dim_plano_conta.md)
* [04_ft_resultado.md](../scripts/powerquery/04_ft_resultado.md)
* [05_dim_calendario.md](../scripts/powerquery/05_dim_calendario.md)

### 📊 DAX

* [kpis.md](../scripts/dax/02_kpis.md)
* [analises.md](../scripts/dax/03_analises.md)
* [simulacoes.md](../scripts/dax/06_simulacoes.md)