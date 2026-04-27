# ⚙️ Power Query (M Language)

Este diretório contém os scripts responsáveis pela ingestão, transformação e estruturação dos dados no Power BI.

## 📂 Estrutura

- 📌 Parâmetros  
  👉 [01_parametros.md](./01_parametros.md)

- 📄 Extração de dados (PDF)  
  👉 [02_extracao_pdf.md](./02_extracao_pdf.md)

- 📊 Dimensão Plano de Contas  
  👉 [03_dim_plano_conta.md](./03_dim_plano_conta.md)

- 🧾 Tabela Fato (Resultado)  
  👉 [04_ft_resultado.md](./04_ft_resultado.md)

- 📅 Dimensão Calendário  
  👉 [05_dim_calendario.md](./05_dim_calendario.md)

---

## 🔗 Rastreabilidade

Cada script possui referência direta à documentação em `/docs`, permitindo navegação entre:

- Regras de negócio
- Modelagem
- Pipeline de dados

---

## 🧠 Abordagem Técnica

A estrutura segue boas práticas de engenharia de dados:

- Separação por responsabilidade (extração, transformação, modelagem)
- Preparação para modelo dimensional (Star Schema)
- Organização compatível com pipelines (Data Engineering mindset)
