# 🔹 Parâmetro Caminho Pasta

## 🎯 Objetivo

Centralizar variáveis reutilizáveis para facilitar manutenção e portabilidade do projeto.

---

## ⚙️ Implementação

```powerquery
// =========================================================
// Projeto: DRE Automatizada em Power BI
//
// Objetivo:
// - Centralizar o caminho da origem dos arquivos
// - Facilitar manutenção e atualização do projeto
// - Permitir reutilização do parâmetro nas queries
//
// 🔗 Rastreabilidade:
// - Documento técnico:
//   ../docs/04_desenvolvimento.md
//
// - Artigo:
//   ../docs/10_artigo_tecnico.md
//   4.2 Criação de Parâmetro
//   4.2.1 Justificativa para o Negócio
//
// Utilização:
// - Basepdf
// - dPlanoConta
//
// Benefícios:
// - Redução de hardcode
// - Maior portabilidade
// - Facilidade de manutenção
// =========================================================


    // =====================================================
    // 1. Definição do caminho base do projeto
    // =====================================================
    // Referência:
    // - 4.2.1 → Definição de parâmetros de ambiente
    //
    // Objetivo:
    // - Centralizar o diretório raiz das fontes de dados
    // - Evitar hardcode em múltiplas queries
    // - Facilitar migração de ambiente


        "D:\DRE Embraer"  
    meta [
        IsParameterQuery = true,
        Type = "Text",
        IsParameterQueryRequired = true
    ]
```
## 🧠 Observações

- Evita hardcode em múltiplas queries
- Facilita mudança de ambiente (local → cloud)
- Boa prática para escalabilidade
