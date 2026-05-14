# 🔹 Tabela Fato: Resultado

## 🎯 Objetivo

Transformar dados extraídos em formato analítico (modelo fato).

---

## ⚙️ Implementação

```powerquery

// =========================================================
// Projeto: DRE Automatizada em Power BI
//
// Objetivo:
// - Construir tabela fato da DRE
// - Converter dados financeiros para formato analítico
// - Integrar fato com dimensão de contas
//
// 🔗 Rastreabilidade:
// - Documento técnico:
//   ../docs/04_desenvolvimento.md
//   ../docs/05_dicionario.md
//
// - Artigo:
//   ../docs/10_artigo_tecnico.md
//   4.5 Transformações – ftResultado
//   4.5.1 Etapas e justificativas
//   5.2 Tabela ftResultado
//
// Estrutura:
// Basepdf → Unpivot → Join → Fato Analítica
// =========================================================

let

    // =====================================================
    // 1. Leitura da base analítica (Basepdf)
    // =====================================================
    // Referência:
    // - 4.5 → Estruturação da tabela fato
    //
    // Objetivo:
    // - Utilizar base estruturada extraída dos PDFs como origem

    Fonte =
        Basepdf,


    // =====================================================
    // 2. Padronização dos nomes das colunas
    // =====================================================
    // Referência:
    // - 4.5.1.1 → Normalização de estrutura tabular
    //
    // Objetivo:
    // - Renomear colunas para padrão analítico
    // - Facilitar unpivot e modelagem dimensional

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


    // =====================================================
    // 3. Transformação para formato analítico (Unpivot)
    // =====================================================
    // Referência:
    // - 4.5.1.2 → Conversão para modelo estrela (long format)
    //
    // Objetivo:
    // - Transformar colunas de período em linhas
    // - Facilitar análises temporais

    UnpivotYears =
        Table.UnpivotOtherColumns(
            RenameColumns,
            {"ID Conta", "Descrição da Conta"},
            "Data",
            "Valor"
        ),


    // =====================================================
    // 4. Padronização de tipos de dados
    // =====================================================
    // Objetivo:
    // - Garantir consistência para cálculos e modelagem

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


    // =====================================================
    // 5. Integração com dimensão dPlanoConta
    // =====================================================
    // Referência:
    // - 4.5.1.3 → Relacionamento com dimensão de contas
    //
    // Objetivo:
    // - Enriquecer fato com atributos hierárquicos
    // - Permitir análises por estrutura da DRE

    MergePlanoConta =
        Table.NestedJoin(
            ChangeType,
            {"ID Conta"},
            dPlanoConta,
            {"ID Conta"},
            "PlanoConta",
            JoinKind.LeftOuter
        ),


    // =====================================================
    // 6. Expansão da dimensão de contas
    // =====================================================
    // Objetivo:
    // - Trazer atributos necessários da dimensão

    ExpandPlanoConta =
        Table.ExpandTableColumn(
            MergePlanoConta,
            "PlanoConta",
            {"Lançamento"},
            {"Lançamento"}
        ),


    // =====================================================
    // 7. Filtragem de lançamentos válidos
    // =====================================================
    // Referência:
    // - 4.5.1.4 → Aplicação de regras de negócio
    //
    // Objetivo:
    // - Manter apenas registros relevantes para análise financeira
    // - Remover períodos de ajuste ou inconsistências

    FilterLancamentos =
        Table.SelectRows(
            ExpandPlanoConta,
            each
                [Lançamento] = 1
                and [Data] <> #date(2021, 12, 31)
        ),


    // =====================================================
    // 8. Remoção de colunas desnecessárias
    // =====================================================
    // Objetivo:
    // - Reduzir redundância no modelo final
    // - Otimizar performance do modelo

    RemoveColumns =
        Table.RemoveColumns(
            FilterLancamentos,
            {"Descrição da Conta", "Lançamento"}
        )

in
    RemoveColumns

```
## 🧠 Observações

- Conversão para formato analítico (unpivot)
- Integração com dimensão (join)
- Filtragem de dados relevantes
