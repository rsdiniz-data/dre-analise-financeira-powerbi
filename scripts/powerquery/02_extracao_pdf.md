# 🔹 Extração de Dados (PDF)

📄 Referência: docs/04_desenvolvimento.md | Seção 4.4

## 🎯 Objetivo

Extrair e estruturar dados da DRE a partir de arquivos PDF.

---

## ⚙️ Implementação

```powerquery
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
```
## 🧠 Observações

- Uso de Pdf.Tables() para leitura estruturada
- Filtragem direcionada às tabelas da DRE
- Preparação para transformação analítica (unpivot)
