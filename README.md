# 📊 DRE Automatizada | Data Analytics & Engineering

## 🚀 Visão Geral

Transformei um processo manual de análise financeira (baseado em PDFs e Excel) em uma solução analítica automatizada, com pipeline estruturado, modelo dimensional e dashboard interativo em Power BI.

---

## ⚠️ Problema de Negócio

- Dados financeiros em formatos não estruturados  
- Alto esforço manual e risco de erros  
- Baixa padronização  
- Dificuldade de análise histórica e comparativa  

---

## ✅ Solução

Desenvolvimento de uma solução completa de dados, envolvendo:

- Pipeline de ingestão e transformação (Power Query)  
- Modelagem dimensional (Star Schema)  
- Construção de métricas financeiras em DAX  
- Dashboard interativo para análise e tomada de decisão  

---

## 🧠 Stack Utilizada

- Power BI  
- Power Query (M)  
- DAX  
- Modelagem Dimensional  

---

## 📊 Entregas

- KPIs financeiros: Receita, Custos, EBITDA, Lucro Líquido  
- Análises: YoY, AH (Horizontal) e AV (Vertical)  
- Simulações de cenário (What-If)  
- Dashboard interativo  

🔗 [Acessar Dashboard](https://app.powerbi.com/view?r=eyJrIjoiOTcwN2E4OTMtNGUxMS00MDBjLTg3MjMtNzQzOWM0OWE0Y2I0IiwidCI6IjE2YjQyY2M1LTJiZWUtNDRjZS05MWE4LWYyMjgwMGRkZmZmYyJ9)

---

## 💼 Valor Gerado

- Redução de esforço manual na consolidação de dados  
- Aumento da confiabilidade das informações  
- Base estruturada para análises escaláveis  
- Suporte direto à tomada de decisão  

---

## 🔗 Explorar Projeto

- 📄 [Documentação técnica](./docs/README.md)  
- 💻 [Scripts (DAX & Power Query)](./scripts/README.md)  
- 📢 [Artigo no LinkedIn](https://www.linkedin.com/pulse/dre-automatizada-em-power-bi-do-operacional-ao-ricardo-diniz-mpjjf/)

---

## 🎯 Destaque

Este projeto demonstra a integração entre Data Analytics e Engenharia de Dados na construção de soluções orientadas ao negócio.



---

# 📊 DRE Automatizada – Análise Financeira

## 🧠 Sobre o Projeto

Desenvolvi um projeto de Business Intelligence focado na construção de uma DRE automatizada em Power BI, com o objetivo de transformar dados financeiros em suporte real à tomada de decisão.

O projeto substitui processos manuais baseados em planilhas por um modelo estruturado, permitindo análises dinâmicas, rastreabilidade dos dados e maior confiabilidade das informações.

Com o uso de Power Query, modelagem dimensional e DAX, foram construídos indicadores como Receita, Custos, EBITDA e Lucro Líquido, além de análises de variação (YoY, AH e AV) e simulações de cenários (What-If) para apoio estratégico.

---

## 🔗 Navegação

- 📊 [Acessar dashboard interativo](https://app.powerbi.com/view?r=eyJrIjoiOTcwN2E4OTMtNGUxMS00MDBjLTg3MjMtNzQzOWM0OWE0Y2I0IiwidCI6IjE2YjQyY2M1LTJiZWUtNDRjZS05MWE4LWYyMjgwMGRkZmZmYyJ9)

- 📄 [Ver documentação técnica](./docs/README.md)

- 💻 [Explorar scripts](./scripts/README.md)

---

## 📢 Publicação no LinkedIn

Este projeto também foi apresentado em formato de artigo, com foco no contexto de negócio e geração de valor:

- 📢 [Ler artigo completo](https://www.linkedin.com/pulse/dre-automatizada-em-power-bi-do-operacional-ao-ricardo-diniz-mpjjf/)

---

## 🎯 Valor para o Negócio

O dashboard permite:

* Identificar tendências de desempenho financeiro
* Analisar a estrutura de custos e rentabilidade
* Avaliar impactos de decisões antes da execução
* Apoiar a priorização de iniciativas com maior geração de valor

---

## 🏗️ Arquitetura da Solução

Modelo dimensional (Star Schema):

* Fato: `ftResultado`
* Dimensões: `dPlanoConta`, `dCalendario`

---

## 🔄 Pipeline de Dados

1. Ingestão de dados (PDF e Excel)
2. Transformações no Power Query
3. Modelagem dimensional
4. Criação de métricas em DAX

---

## 🧾 Scripts e Rastreabilidade

Os scripts utilizados no projeto estão organizados nas seguintes pastas:

* [/scripts/powerquery](./scripts/powerquery) → Transformações de dados
* [/scripts/dax](./scripts/dax) → Métricas e indicadores

A solução foi documentada de forma a permitir rastreabilidade completa entre:

- Documentação técnica ([/docs](./docs))
- Scripts ([/scripts](./scripts))
- Implementação no Power BI

Cada script contém referências diretas às seções da documentação, facilitando a validação técnica da solução.

---

## 📊 KPIs

* Receita Bruta
* Custos
* Despesas
* EBITDA
* EBIT
* Lucro Líquido

---

## 🔮 Simulação de Cenários

Análises What-If permitem avaliar impactos no resultado com base em variações de:

* Receita
* Custos
* Despesas

---

## 📸 Dashboard

![Dashboard DRE](images/Dashboard_1_DRE.png)
![Simulador](images/Dashboard_2_Simulador.png)

---

## 💡 Conclusão

Este projeto reforça como Business Intelligence pode ir além da visualização, atuando como ferramenta de gestão, estratégia e governança de dados.
