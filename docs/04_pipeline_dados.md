# 4. Desenvolvimento do Projeto
4.1 Fontes de Dados
- PDFs contendo a DRE (demonstrações financeiras)
- Planilhas Excel com plano de contas

---

## 4.2 Pipeline de Dados

O pipeline foi estruturado em etapas bem definidas:

- Ingestão → leitura de arquivos locais (PDF e Excel)
- Extração → identificação e captura das tabelas da DRE nos PDFs
- Transformação → limpeza, padronização e estruturação dos dados
- Carga → organização final no modelo dimensional

---

## 4.3 Modelagem de Dados

A modelagem foi estruturada seguindo o padrão Star Schema, com separação entre tabela fato e dimensões, permitindo análises eficientes e escaláveis.

Estrutura do Modelo
- Tabela Fato
  - ftResultado → armazena valores financeiros por conta e data
- Dimensões
  - dPlanoConta → estrutura hierárquica da DRE (N1, N2, N3)
  - dCalendario → suporte a análises temporais (Ano, Mês)

---

## 4.4 Transformações Aplicadas

Durante a preparação dos dados, foram aplicadas as seguintes transformações:

- Unpivot de colunas
  Conversão de colunas de anos para formato linha (modelo analítico)
- Hierarquia contábil
  Construção dos níveis N1, N2 e N3 com base no código da conta
- Classificação de contas
  Identificação da natureza financeira (Receita vs Custos/Despesas)

---

## 4.5 Regras de Negócio

- Exclusão de contas sintéticas
- Consideração apenas de contas analíticas (Lançamento = 1)
- Padronização de tipos de dados
- Enriquecimento da tabela fato via relacionamento com dimensão

---

## 4.6 Implementação Técnica

As transformações foram implementadas utilizando Power Query (M), organizadas por responsabilidade:

- [Extração de dados (PDF)](../scripts/powerquery/02_extracao_pdf.md)
- [Dimensão Plano de Contas](../scripts/powerquery/03_dim_plano_conta.md)
- [Tabela Fato (Resultado)](../scripts/powerquery/04_ft_resultado.md)
- [Dimensão Calendário](../scripts/powerquery/05_dim_calendario.md)

📄 Ver visão completa:  [Explorar documentação Power Query](../scripts/powerquery/README.md)

## 🔗 Rastreabilidade

---

A solução foi estruturada garantindo rastreabilidade completa entre:

- Fonte de dados → Transformação → Modelagem → Análise

Essa abordagem permite:

- Transparência na construção dos dados
- Facilidade de manutenção
- Validação técnica ponta a ponta

# 4. Pipeline de Dados

## 4.1 Fontes de Dados

- PDFs contendo a DRE (demonstrações financeiras)
- Planilhas Excel com plano de contas

---

## 4.2 Etapas do Pipeline

O pipeline foi estruturado em etapas bem definidas:

- **Ingestão** → leitura de arquivos locais (PDF e Excel)  
- **Extração** → identificação e captura das tabelas da DRE nos PDFs  
- **Transformação** → limpeza, padronização e modelagem dos dados  
- **Carga** → estruturação final no modelo dimensional (Star Schema)

---

## 4.3 Implementação Técnica

Os scripts foram organizados por responsabilidade, seguindo boas práticas de engenharia de dados.

📄 Ver detalhes: [Explorar documentação Power Query](../scripts/powerquery/README.md)

---

## 🔗 Rastreabilidade

Cada etapa do pipeline está diretamente conectada à documentação e aos scripts:

- A **extração** está documentada em → seção 4.2  
- A **transformação e modelagem** estão detalhadas em → seção 5  
- A **implementação técnica** pode ser validada diretamente nos scripts acima  

Essa abordagem garante rastreabilidade completa entre regra de negócio, modelagem e implementação.
