# 🔹 Dimensão: Plano de Contas

## 🎯 Objetivo

Construir a dimensão hierárquica da DRE para suportar análises financeiras.

---

## ⚙️ Implementação

```powerquery

// =========================================================
// Projeto: DRE Automatizada em Power BI
//
// Objetivo:
// - Construir dimensão hierárquica da DRE
// - Estruturar níveis analíticos do plano de contas
// - Classificar indicadores financeiros
//
// 🔗 Rastreabilidade:
// - Documento técnico:
//   ../docs/04_desenvolvimento.md
//   ../docs/05_dicionario.md
//
// - Artigo:
//   ../docs/10_artigo_tecnico.md
//   4.4 Transformações – dPlanoConta
//   5.1 Tabela dPlanoConta
//
// Estrutura:
// PlanoConta → Hierarquia → Classificação → Dimensão
// =========================================================

let

    // =====================================================
    // 1. Leitura da base de plano de contas
    // =====================================================
    // Referência:
    // - 4.4 → Estruturação da dimensão dPlanoConta
    //
    // Objetivo:
    // - Carregar arquivo Excel com estrutura do plano de contas

    Fonte =
        Excel.Workbook(
            File.Contents(CaminhoPasta & "\Bases\PlanoContas.xlsx"),
            null,
            true
        ),


    // =====================================================
    // 2. Seleção da tabela de plano de contas
    // =====================================================
    // Objetivo:
    // - Extrair tabela estruturada do arquivo Excel

    PlanoConta =
        Fonte{[Item = "PlanoConta", Kind = "Table"]}[Data],


    // =====================================================
    // 3. Cálculo do tamanho do código da conta
    // =====================================================
    // Referência:
    // - 4.4.1.2 → Identificação de níveis hierárquicos
    //
    // Objetivo:
    // - Determinar profundidade da hierarquia (N1, N2, N3)

    AddComprimento =
        Table.AddColumn(
            PlanoConta,
            "Comprimento",
            each Text.Length([ID Conta]),
            Int64.Type
        ),


    // =====================================================
    // 4. Construção do nível N1 (nível macro)
    // =====================================================
    // Objetivo:
    // - Identificar grupo principal da DRE

    AddN1 =
        Table.AddColumn(
            AddComprimento,
            "N1",
            each if [Comprimento] = 4 then [Descrição] else null
        ),


    // =====================================================
    // 5. Construção do nível N2 (subgrupo)
    // =====================================================
    // Referência:
    // - 4.4.1.3 → Estrutura intermediária da hierarquia
    //
    // Objetivo:
    // - Definir subcategorias dentro do grupo principal

    AddN2 =
        Table.AddColumn(
            AddN1,
            "N2",
            each
                if [Comprimento] = 7 then [Descrição]
                else if [Comprimento] = 4 then "XXX"
                else null
        ),


    // =====================================================
    // 6. Construção do nível N3 (detalhamento)
    // =====================================================
    // Objetivo:
    // - Representar nível analítico mais detalhado

    AddN3 =
        Table.AddColumn(
            AddN2,
            "N3",
            each if [Comprimento] = 10 then [Descrição] else null
        ),


    // =====================================================
    // 7. Preenchimento da hierarquia
    // =====================================================
    // Referência:
    // - 4.4.1.4 → Consolidação hierárquica
    //
    // Objetivo:
    // - Propagar níveis superiores para linhas inferiores

    FillHierarchy =
        Table.FillDown(
            AddN3,
            {"N1", "N2"}
        ),


    // =====================================================
    // 8. Remoção de marcador auxiliar
    // =====================================================
    // Objetivo:
    // - Limpar valores temporários usados na construção da hierarquia

    RemoveMarcador =
        Table.ReplaceValue(
            FillHierarchy,
            "XXX",
            null,
            Replacer.ReplaceValue,
            {"N2"}
        ),


    // =====================================================
    // 9. Criação do código DRE
    // =====================================================
    // Referência:
    // - 4.4.1.5 → Identificação de agrupadores da DRE
    //
    // Objetivo:
    // - Definir código base de consolidação financeira

    AddCodDRE =
        Table.AddColumn(
            RemoveMarcador,
            "CodDRE",
            each if [Comprimento] = 4 then [ID Conta] else null
        ),


    // =====================================================
    // 10. Preenchimento do código DRE
    // =====================================================
    // Objetivo:
    // - Propagar código DRE para estrutura hierárquica

    FillCodDRE =
        Table.FillDown(
            AddCodDRE,
            {"CodDRE"}
        ),


    // =====================================================
    // 11. Padronização de tipos de dados
    // =====================================================
    // Objetivo:
    // - Garantir consistência para modelagem analítica

    ChangeType =
        Table.TransformColumnTypes(
            FillCodDRE,
            {
                {"CodDRE", type text},
                {"ID Conta", type text},
                {"Lançamento", Int64.Type},
                {"Descrição", type text},
                {"N1", type text},
                {"N2", type text},
                {"N3", type text},
                {"Calculado", Int64.Type}
            }
        ),


    // =====================================================
    // 12. Classificação do tipo de indicador
    // =====================================================
    // Referência:
    // - 4.4.1.6 → Classificação financeira (receita vs custo/despesa)
    //
    // Objetivo:
    // - Definir sinal do indicador para análises financeiras

    AddTipoIndicador =
        Table.AddColumn(
            ChangeType,
            "TipoIndicador",
            each
                if [CodDRE] = "3.02" or [CodDRE] = "3.04"
                then -1
                else 1,
            Int64.Type
        ),


    // =====================================================
    // 13. Remoção de coluna auxiliar
    // =====================================================
    // Objetivo:
    // - Limpar coluna técnica usada apenas para cálculo de hierarquia

    RemoveComprimento =
        Table.RemoveColumns(
            AddTipoIndicador,
            {"Comprimento"}
        )

in
    RemoveComprimento

```
## 🧠 Observações

- Construção de hierarquia (N1, N2, N3)
- Classificação de indicadores (receita vs custo/despesa)
- Base para cálculo de KPIs
