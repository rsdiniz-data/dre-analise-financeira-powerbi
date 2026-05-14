# 6. Mapeamento de Indicadores (KPIs)

## 🎯 Objetivo
Estabelecer a estrutura conceitual dos indicadores financeiros antes da implementação técnica em DAX, garantindo alinhamento entre regras de negócio, modelagem dimensional e necessidades da Diretoria Financeira.

> “O processo se inicia com a identificação do principal stakeholder [...] seguido da definição do KPI central do projeto — o Resultado Líquido do Exercício (Lucro Líquido).”

---

## 👤 Stakeholder e KPI Central
- **Stakeholder principal:** Diretoria Financeira / Controladoria  
- **KPI central:** **Lucro Líquido**  
- **Processos monitorados:**  
  - Geração de receita  
  - Eficiência operacional  
  - Rentabilidade  

Esse mapeamento orienta a priorização dos indicadores e assegura que o modelo reflita corretamente a lógica contábil da DRE.

---

## 🧱 Estrutura dos Indicadores
Os KPIs foram definidos com base na hierarquia contábil e na modelagem dimensional:

- Tabela fato **ftResultado**  
- Dimensão **dPlanoConta**  
- Hierarquia da DRE (N1, N2, N3)  
- Classificação contábil (**CodDRE**, **TipoIndicador**)  

> “Esse procedimento é fundamental para demonstrar compreensão do contexto financeiro antes da etapa técnica.”

---

## 📊 KPIs Financeiros Mapeados
Indicadores estruturados no projeto:

- Receita Bruta  
- Custos  
- Despesas  
- Margem Bruta  
- EBIT  
- EBITDA  
- Lucro Líquido  

Esses KPIs sustentam análises de desempenho, eficiência e rentabilidade.

---

## 🔗 Rastreabilidade
O mapeamento formaliza definições, reduz ambiguidades e garante reprodutibilidade:

> “O mapeamento formaliza as definições dos indicadores, reduz ambiguidades e permite replicar o processo de levantamento de requisitos em projetos futuros.”

Fluxo completo:  
**Fonte de Dados → Transformação → Modelagem → KPI**
