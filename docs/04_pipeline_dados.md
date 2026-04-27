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

Os scripts foram organizados por responsabilidade, seguindo boas práticas de engenharia de dados:

- 📌 Parâmetros  
  👉 [01_parametros.md](../scripts/powerquery/01_parametros.md)

- 📄 Extração de dados (PDF)  
  👉 [02_extracao_pdf.md](../scripts/powerquery/02_extracao_pdf.md)

- 📊 Dimensão Plano de Contas  
  👉 [03_dim_plano_conta.md](../scripts/powerquery/03_dim_plano_conta.md)

- 🧾 Tabela Fato (Resultado)  
  👉 [04_ft_resultado.md](../scripts/powerquery/04_ft_resultado.md)

- 📅 Dimensão Calendário  
  👉 [05_dim_calendario.md](../scripts/powerquery/05_dim_calendario.md)

---

## 🔗 Rastreabilidade

Cada etapa do pipeline está diretamente conectada à documentação e aos scripts:

- A **extração** está documentada em → seção 4.2  
- A **transformação e modelagem** estão detalhadas em → seção 5  
- A **implementação técnica** pode ser validada diretamente nos scripts acima  

Essa abordagem garante rastreabilidade completa entre regra de negócio, modelagem e implementação.
