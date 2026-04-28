# 🔹 Dimensão: Plano de Contas

📄 Referência: docs/04_desenvolvimento.md | Seção 4.2 e 4.4 e docs/05_dicionario.md | Seção 5.1

## 🎯 Objetivo

Construir a dimensão hierárquica da DRE para suportar análises financeiras.

---

## ⚙️ Implementação

```powerquery
let
    Fonte =
        Excel.Workbook(
            File.Contents(CaminhoPasta & "\Bases\PlanoContas.xlsx"),
            null,
            true
        ),

    PlanoConta =
        Fonte{[Item="PlanoConta",Kind="Table"]}[Data],

    AddComprimento =
        Table.AddColumn(
            PlanoConta,
            "Comprimento",
            each Text.Length([ID Conta]),
            Int64.Type
        ),

    AddN1 =
        Table.AddColumn(
            AddComprimento,
            "N1",
            each if [Comprimento] = 4 then [Descrição] else null
        ),

    AddN2 =
        Table.AddColumn(
            AddN1,
            "N2",
            each if [Comprimento] = 7 then [Descrição]
            else if [Comprimento] = 4 then "XXX"
            else null
        ),

    AddN3 =
        Table.AddColumn(
            AddN2,
            "N3",
            each if [Comprimento] = 10 then [Descrição] else null
        ),

    FillHierarchy =
        Table.FillDown(AddN3, {"N1","N2"}),

    RemoveMarcador =
        Table.ReplaceValue(
            FillHierarchy,
            "XXX",
            null,
            Replacer.ReplaceValue,
            {"N2"}
        ),

    AddCodDRE =
        Table.AddColumn(
            RemoveMarcador,
            "CodDRE",
            each if [Comprimento] = 4 then [ID Conta] else null
        ),

    FillCodDRE =
        Table.FillDown(AddCodDRE, {"CodDRE"}),

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

    AddTipoIndicador =
        Table.AddColumn(
            ChangeType,
            "TipoIndicador",
            each if [CodDRE] = "3.02" or [CodDRE] = "3.04"
            then -1
            else 1,
            Int64.Type
        ),

    RemoveComprimento =
        Table.RemoveColumns(AddTipoIndicador, {"Comprimento"})
in
    RemoveComprimento
```
## 🧠 Observações

- Construção de hierarquia (N1, N2, N3)
- Classificação de indicadores (receita vs custo/despesa)
- Base para cálculo de KPIs
