# 🔹 Tabela Fato: Resultado

📄 Referência: docs/04_pipeline_dados.md    
📄 Referência: docs/05_modelagem.md

## 🎯 Objetivo

Transformar dados extraídos em formato analítico (modelo fato).

---

## ⚙️ Implementação

```powerquery
let
    Fonte = Basepdf,

    RenameColumns =
        Table.RenameColumns(
            Fonte,
            {
                {"Código da#(lf)Conta", "ID Conta"},
                {"Último Exercício#(lf)01/01/2022 à 31/12/2022", "31/12/2022"},
                {"Penúltimo Exercício#(lf)01/01/2021 à 31/12/2021", "31/12/2021"},
                {"Último Exercício#(lf)01/01/2024 à 31/12/2024", "31/12/2024"},
                {"Penúltimo Exercício#(lf)01/01/2023 à 31/12/2023", "31/12/2023"}
            }
        ),

    UnpivotYears =
        Table.UnpivotOtherColumns(
            RenameColumns,
            {"ID Conta", "Descrição da Conta"},
            "Data",
            "Valor"
        ),

    ChangeType =
        Table.TransformColumnTypes(
            UnpivotYears,
            {
                {"ID Conta", type text},
                {"Descrição da Conta", type text},
                {"Data", type date},
                {"Valor", type number}
            }
        ),

    MergePlanoConta =
        Table.NestedJoin(
            ChangeType,
            {"ID Conta"},
            dPlanoConta,
            {"ID Conta"},
            "PlanoConta",
            JoinKind.LeftOuter
        ),

    ExpandPlanoConta =
        Table.ExpandTableColumn(
            MergePlanoConta,
            "PlanoConta",
            {"Lançamento"},
            {"Lançamento"}
        ),

    FilterLancamentos =
        Table.SelectRows(
            ExpandPlanoConta,
            each [Lançamento] = 1 and [Data] <> #date(2021,12,31)
        ),

    RemoveColumns =
        Table.RemoveColumns(
            FilterLancamentos,
            {"Descrição da Conta", "Lançamento"}
        )
in
    RemoveColumns
