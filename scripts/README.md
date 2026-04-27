# 💻 Scripts do Projeto

Este diretório contém toda a implementação técnica da solução, organizada por camada de responsabilidade — desde a ingestão e transformação dos dados até a construção das métricas analíticas.

---

## 📂 Estrutura

### ⚙️ /powerquery
Responsável pelo pipeline de dados (ETL):

- Ingestão de dados a partir de PDFs e Excel  
- Extração e estruturação das informações  
- Limpeza e padronização dos dados  
- Construção da tabela fato (`ftResultado`)  
- Criação das dimensões (`dPlanoConta`, `dCalendario`)  

📄 [Explorar documentação Power Query](./powerquery/README.md)

---

### 📊 /dax
Responsável pela camada analítica do modelo:

- KPIs financeiros (Receita, Custos, EBITDA, Lucro Líquido)  
- Análises (AH, AV, YoY)  
- Simulações de cenário (What-If)  
- Medidas auxiliares para suporte à visualização  

📄 [Explorar documentação DAX](./dax/README.md)

---

## 🔗 Rastreabilidade

Os scripts foram desenvolvidos com rastreabilidade completa em relação à documentação do projeto:

- 📄 `/docs` → definição conceitual e regras de negócio  
- 💻 `/scripts` → implementação técnica  

Cada script contém referências diretas às seções da documentação, permitindo navegar facilmente entre conceito e código e facilitando a validação técnica da solução.

---

## 🎯 Objetivo

Organizar a lógica do projeto de forma modular, separando claramente:

- Camada de dados (ingestão e transformação)  
- Camada analítica (cálculo e métricas)  

Essa abordagem melhora a legibilidade, manutenção e escalabilidade da solução, além de refletir boas práticas utilizadas em projetos de dados.
