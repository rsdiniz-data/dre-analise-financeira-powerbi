# 🔹 Parâmetros

📄 Referência: docs/04_pipeline_dados.md

## 🎯 Objetivo

Centralizar variáveis reutilizáveis para facilitar manutenção e portabilidade do projeto.

---

## ⚙️ Implementação

```powerquery
CaminhoPasta =
"D:\DRE Embraer"
meta [IsParameterQuery=true, Type="Text", IsParameterQueryRequired=true]
```
## 🧠 Observações

- Evita hardcode em múltiplas queries
- Facilita mudança de ambiente (local → cloud)
- Boa prática para escalabilidade
