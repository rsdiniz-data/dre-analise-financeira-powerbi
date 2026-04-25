```m
// =========================================================
// PROJETO: DRE Automatizada
// ARQUIVO: transformacoes.md
// =========================================================


// =========================================================
// 🔹 PARÂMETRO
// Referência: docs/04_pipeline_dados.md | Seção 4.1
// =========================================================

CaminhoPasta =
"D:\OneDrive - datafive.com.br\Projetos de BI\DRE Embraer"
meta [IsParameterQuery=true, Type="Text", IsParameterQueryRequired=true]


// =========================================================
// 🔹 EXTRAÇÃO DE DADOS (PDF)
// Referência: docs/04_pipeline_dados.md | Seção 4.2.1 e 4.2.2
// =========================================================

Basepdf =
let
    Fonte = Folder.Files(CaminhoPasta & "\Bases"),

    FilterPDF =
        Table.SelectRows(Fonte, each [Extension] = ".pdf"),

    ExtractTables =
        Table.AddColumn(FilterPDF, "Tables", each Pdf.Tables([Content])),

    ExpandTables =
        Table.ExpandTableColumn(
            ExtractTables,
            "Tables",
            {"Id","Name","Kind","Data"},
            {"Id","TableName","Kind","Data"}
        ),

    FilterDRETables =
        Table.SelectRows(
            ExpandTables,
            each [TableName] = "Table018 (Page 16)"
              or [TableName] = "Table019 (Page 16)"
        ),

    PromoteHeaders =
        Table.AddColumn(
            FilterDRETables,
            "Dados",
            each Table.PromoteHeaders([Data])
        ),

    SelectColumns =
        Table.SelectColumns(PromoteHeaders, {"Dados"}),

    ExpandData =
        Table.ExpandTableColumn(
            SelectColumns,
            "Dados",
            {
                "Código da#(lf)Conta",
                "Descrição da Conta",
                "Último Exercício#(lf)01/01/2022 à 31/12/2022",
                "Penúltimo Exercício#(lf)01/01/2021 à 31/12/2021",
                "Último Exercício#(lf)01/01/2024 à 31/12/2024",
                "Penúltimo Exercício#(lf)01/01/2023 à 31/12/2023"
            }
        )
in
    ExpandData


// =========================================================
// 🔹 DIMENSÃO: PLANO DE CONTAS
// Referência: docs/05_modelagem.md | Seção 5.1 e 5.2
// =========================================================

dPlanoConta =
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


// =========================================================
// 🔹 TABELA FATO
// Referência: docs/04_pipeline_dados.md | Seção 4.2.3 e docs/05_modelagem.md
// =========================================================

ftResultado =
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


// =========================================================
// 🔹 DIMENSÃO CALENDÁRIO
// Referência: docs/05_modelagem.md | Seção 5.3
// =========================================================

dCalendario =
let
    MinDate = List.Min(ftResultado[Data]),
    MaxDate = List.Max(ftResultado[Data]),

    StartDate = Date.StartOfYear(MinDate),
    EndDate = Date.EndOfYear(MaxDate),

    TotalDays = Duration.Days(EndDate - StartDate) + 1,

    DateList =
        List.Dates(
            StartDate,
            TotalDays,
            #duration(1,0,0,0)
        ),

    CalendarTable =
        #table(
            type table[
                Data = date,
                Ano = Int64.Type,
                Mes = text,
                Mes_Num = Int64.Type
            ],
            List.Transform(
                DateList,
                each {
                    _,
                    Date.Year(_),
                    Text.Proper(Text.Start(Date.MonthName(_),3)),
                    Date.Month(_)
                }
            )
        )
in
    CalendarTable
```
