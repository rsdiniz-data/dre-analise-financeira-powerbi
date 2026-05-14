# 🔹 Extração de Dados (PDF)

## 🎯 Objetivo

Extrair e estruturar dados da DRE a partir de arquivos PDF.

---

## ⚙️ Implementação

```powerquery
// =========================================================
// Projeto: DRE Automatizada em Power BI
//
// Objetivo:
// - Ler arquivos PDF da DRE
// - Extrair tabelas financeiras automaticamente
// - Estruturar dados para transformação analítica
//
// 🔗 Rastreabilidade:
// - Documento técnico:
//   ../docs/04_desenvolvimento.md
//
// - Artigo:
//   ../docs/10_artigo_tecnico.md
//   4.1 Coleta e Integração de Dados
//   4.3 Transformações – Basepdf
//
// Processo:
// PDF → Extração → Estruturação → Base Analítica
// =========================================================

let

    // =====================================================
    // 1. Leitura dos arquivos da pasta base
    // =====================================================
    // Referência:
    // - 4.1 → Coleta de dados estruturados e não estruturados
    //
    // Objetivo:
    // - Acessar diretório base do projeto
    // - Carregar arquivos disponíveis para processamento

    Fonte =
        Folder.Files(CaminhoPasta & "\Bases"),


    // =====================================================
    // 2. Filtragem de arquivos PDF
    // =====================================================
    // Referência:
    // - 4.1 → Seleção de fontes válidas de dados
    //
    // Objetivo:
    // - Garantir processamento apenas de arquivos PDF

    FilterPDF =
        Table.SelectRows(
            Fonte,
            each [Extension] = ".pdf"
        ),


    // =====================================================
    // 3. Extração de tabelas dos PDFs
    // =====================================================
    // Referência:
    // - 4.3.1 → Extração de estruturas tabulares do PDF
    //
    // Objetivo:
    // - Converter conteúdo PDF em tabelas estruturadas

    ExtractTables =
        Table.AddColumn(
            FilterPDF,
            "Tables",
            each Pdf.Tables([Content])
        ),


    // =====================================================
    // 4. Expansão das tabelas extraídas
    // =====================================================
    // Objetivo:
    // - Normalizar estrutura de saída do Pdf.Tables
    // - Permitir filtragem por tabela específica

    ExpandTables =
        Table.ExpandTableColumn(
            ExtractTables,
            "Tables",
            {"Id", "Name", "Kind", "Data"},
            {"Id", "TableName", "Kind", "Data"}
        ),


    // =====================================================
    // 5. Seleção das tabelas da DRE
    // =====================================================
    // Referência:
    // - 4.3.1.4 → Identificação de tabelas relevantes da DRE
    //
    // Objetivo:
    // - Filtrar apenas tabelas contábeis relevantes

    FilterDRETables =
        Table.SelectRows(
            ExpandTables,
            each
                [TableName] = "Table018 (Page 16)"
                or [TableName] = "Table019 (Page 16)"
        ),


    // =====================================================
    // 6. Promoção de cabeçalhos
    // =====================================================
    // Referência:
    // - 4.3.1.5 → Normalização de estrutura tabular
    //
    // Objetivo:
    // - Transformar primeira linha em cabeçalho

    PromoteHeaders =
        Table.AddColumn(
            FilterDRETables,
            "Dados",
            each Table.PromoteHeaders([Data])
        ),


    // =====================================================
    // 7. Seleção da coluna estruturada
    // =====================================================
    // Objetivo:
    // - Reduzir estrutura para etapa de expansão

    SelectColumns =
        Table.SelectColumns(
            PromoteHeaders,
            {"Dados"}
        ),


    // =====================================================
    // 8. Expansão final dos dados da DRE
    // =====================================================
    // Referência:
    // - 4.3.2 → Estruturação final da base analítica
    //
    // Objetivo:
    // - Padronizar colunas contábeis para modelagem

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
