# 🔹 Parâmetros

📄 Referência: docs/04_pipeline_dados.md | Seção 4.1

## 🎯 Objetivo

Centralizar variáveis reutilizáveis para facilitar manutenção e portabilidade do projeto.

---

## ⚙️ Implementação

```powerquery
CaminhoPasta =
"D:\Projetos de BI\DRE Embraer"
meta [IsParameterQuery=true, Type="Text", IsParameterQueryRequired=true]
