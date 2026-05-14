# 4. Desenvolvimento do Projeto

## 🔄 Pipeline

O projeto foi estruturado em um pipeline de dados voltado para automatizar a consolidação da DRE, desde a ingestão dos arquivos financeiros até a disponibilização dos dados para análise no Power BI.

Etapas do processo:

1. Ingestão de arquivos PDF e Excel  
2. Extração e tratamento dos dados  
3. Modelagem dimensional (Star Schema)  
4. Construção de métricas e indicadores  
5. Consumo analítico no Power BI  

---

## 📥 Ingestão de Dados

Fontes utilizadas:

- PDFs contendo a DRE (Demonstração do Resultado do Exercício)
- Planilha Excel com o plano de contas

Objetivos da ingestão:

- Centralizar dados financeiros dispersos
- Automatizar atualizações
- Reduzir dependência de processos manuais
- Garantir rastreabilidade da origem dos dados

---

## ⚙️ Transformações (Power Query)

As transformações foram implementadas utilizando Power Query (M), organizadas por responsabilidade.

### 📄 Extração da DRE (PDF)

🔗 Script:  
👉 [02_extracao_pdf.md](../scripts/powerquery/02_extracao_pdf.md)

Principais etapas:

- Leitura automática dos arquivos PDF
- Extração das tabelas financeiras
- Padronização dos cabeçalhos
- Limpeza e estruturação dos dados

Regras aplicadas:

- Filtro apenas de arquivos `.pdf`
- Seleção das tabelas da DRE
- Tratamento de tipos e estrutura analítica

---

### 📊 Dimensão `dPlanoConta`

🔗 Script:  
👉 [03_dim_plano_conta.md](../scripts/powerquery/03_dim_plano_conta.md)

Responsável por:

- Estruturação da hierarquia contábil
- Construção dos níveis `N1`, `N2` e `N3`
- Classificação de contas
- Criação de indicadores auxiliares

Regras aplicadas:

- Identificação de contas analíticas
- Criação da coluna `CodDRE`
- Classificação via `TipoIndicador`

---

### 📈 Tabela Fato `ftResultado`

🔗 Script:  
👉 [04_ft_resultado.md](../scripts/powerquery/04_ft_resultado.md)

Responsável por:

- Estruturação da tabela fato
- Conversão para formato analítico
- Integração com dimensões

Regras aplicadas:

- Unpivot das colunas de anos
- Padronização de tipos
- Join com `dPlanoConta`
- Filtro `Lançamento = 1`

---

### 📅 Dimensão `dCalendario`

🔗 Script:  
👉 [05_dim_calendario.md](../scripts/powerquery/05_dim_calendario.md)

Responsável por:

- Estruturação da dimensão de tempo
- Suporte a análises temporais
- Inteligência de datas

Atributos principais:

- Ano
- Mês
- Número do mês
- Datas contínuas para análises históricas

---

## ⭐ Modelagem Dimensional

O modelo foi estruturado seguindo o padrão Star Schema:

- Fato:
  - `ftResultado`

- Dimensões:
  - `dPlanoConta`
  - `dCalendario`

Relacionamentos:

`dPlanoConta (1) → (N) ftResultado`  
`dCalendario (1) → (N) ftResultado`

📷 ![Modelo Dimensional](../images/modelo_dimensional_star_schema_dre.png)

---

## 📊 Consumo Analítico

Após o processamento e modelagem, os dados foram disponibilizados no Power BI para construção de:

- KPIs financeiros
- Análises históricas
- Comparações anuais (YoY)
- Análise Horizontal (AH)
- Análise Vertical (AV)
- Simulações What-If

---

## 🔗 Rastreabilidade

A solução foi organizada garantindo rastreabilidade completa entre:

- Fonte de dados
- Transformações
- Modelagem
- Métricas
- Visualizações

Essa abordagem facilita:

- Manutenção da solução
- Validação técnica
- Governança dos dados
- Evolução futura da arquitetura