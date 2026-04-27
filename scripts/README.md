# Scripts do Projeto

Este diretório contém toda a implementação técnica do projeto, organizada por camada de responsabilidade.

## Estrutura

### 📊 /dax
Contém as medidas utilizadas no Power BI:

- KPIs financeiros (Receita, Custos, EBITDA, Lucro)
- Análises (AH, AV, YoY)
- Simulações de cenário (What-If)
- Medidas auxiliares

📄 Ver detalhes em: `scripts/dax/README.md`

---

### ⚙️ /powerquery
Contém o pipeline de dados (ETL):

- Extração de dados de PDFs
- Transformações e limpeza
- Construção da tabela fato
- Criação das dimensões

📄 Ver detalhes em: `scripts/powerquery/README.md`

---

## 🔗 Rastreabilidade

Os scripts foram desenvolvidos com rastreabilidade completa em relação à documentação do projeto:

- `/docs` → explicação conceitual e de negócio  
- `/scripts` → implementação técnica  

Cada script contém referências diretas às seções da documentação, facilitando a validação técnica da solução.

---

## 🎯 Objetivo

Organizar a lógica do projeto de forma clara, separando:

- Camada de transformação (ETL)
- Camada analítica (DAX)

Essa separação melhora a manutenção, escalabilidade e entendimento da solução.
