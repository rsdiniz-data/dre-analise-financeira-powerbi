```python
=========================================================    
DCALENDARIO.pq
Projeto: DRE Automatizada em Power BI

Objetivo:
- Criar dimensão calendário dinâmica
- Suportar análises temporais da DRE
- Habilitar inteligência de tempo no Power BI

🔗 Rastreabilidade:
- Documento técnico:
  ../docs/04_desenvolvimento.md
  ../docs/05_dicionario.md

- Artigo:
  ../docs/10_artigo_tecnico.md
  4.6 Transformações – dCalendario
  4.6.1 Etapas e justificativas
  5.3 Tabela dCalendario
  5.3.1 Descrição da Tabela
  5.3.2 Estrutura da Tabela
Estrutura:
dCalendario → ftResultado
=========================================================
```
```python
# =========================================================
# DCALENDARIO.pq
# Projeto: DRE Automatizada em Power BI
#
# Objetivo:
# - Criar dimensão calendário dinâmica
# - Suportar análises temporais da DRE
# - Habilitar inteligência de tempo no Power BI
#
# 🔗 Rastreabilidade:
# - Documento técnico:
#   ../docs/04_desenvolvimento.md
#   ../docs/05_dicionario.md
#
# - Artigo:
#   ../docs/10_artigo_tecnico.md
#   4.6 Transformações – dCalendario
#   4.6.1 Etapas e justificativas
#   5.3 Tabela dCalendario
#   5.3.1 Descrição da Tabela
#   5.3.2 Estrutura da Tabela
#
# Estrutura:
# dCalendario → ftResultado
# =========================================================
```

# 🔹 Dimensão Calendário

## 🎯 Objetivo

Criar dimensão temporal para suportar análises YoY, AH e AV, garantindo continuidade das datas e suporte às funções de inteligência de tempo utilizadas no Power BI.

---

## ⚙️ Implementação

```powerquery

// =========================================================
// DCALENDARIO.pq
// Projeto: DRE Automatizada em Power BI
//
// Objetivo:
// - Criar dimensão calendário dinâmica
// - Suportar análises temporais da DRE
// - Habilitar inteligência de tempo no Power BI
//
// 🔗 Rastreabilidade:
// - Documento técnico:
//   ../docs/04_desenvolvimento.md
//   ../docs/05_dicionario.md
//
// - Artigo:
//   ../docs/10_artigo_tecnico.md
//   4.6 Transformações – dCalendario
//   4.6.1 Etapas e justificativas
//   5.3 Tabela dCalendario
//   5.3.1 Descrição da Tabela
//   5.3.2 Estrutura da Tabela
//
// Estrutura:
// dCalendario → ftResultado
// =========================================================


let

    // =====================================================
    // 1. Identificação do período analisado
    // =====================================================
    // Referência:
    // - 4.6.1.1 → Identificação da menor e maior data
    //
    // Objetivo:
    // - Garantir cobertura completa do período financeiro

    MinDate =
        List.Min(ftResultado[Data]),

    MaxDate =
        List.Max(ftResultado[Data]),


    // =====================================================
    // 2. Expansão para anos completos
    // =====================================================
    // Referência:
    // - 4.6.1.2 → Expansão para anos completos
    //
    // Objetivo:
    // - Garantir consistência das análises anuais

    StartDate =
        Date.StartOfYear(MinDate),

    EndDate =
        Date.EndOfYear(MaxDate),


    // =====================================================
    // 3. Cálculo do total de dias
    // =====================================================
    // Objetivo:
    // - Determinar tamanho da lista contínua de datas

    TotalDays =
        Duration.Days(EndDate - StartDate) + 1,


    // =====================================================
    // 4. Criação da lista contínua de datas
    // =====================================================
    // Referência:
    // - 4.6.1.3 → Criação de lista contínua de datas
    //
    // Objetivo:
    // - Garantir continuidade temporal
    // - Suportar funções DAX de inteligência de tempo

    DateList =
        List.Dates(
            StartDate,
            TotalDays,
            #duration(1,0,0,0)
        ),


    // =====================================================
    // 5. Construção da dimensão calendário
    // =====================================================
    // Referência:
    // - 4.6.1.4 → Criação das colunas Ano, Mês e Mês_Num
    //
    // Objetivo:
    // - Criar atributos temporais para análise

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

                    // Data completa
                    _,

                    // Ano
                    Date.Year(_),

                    // Nome abreviado do mês
                    Text.Proper(
                        Text.Start(
                            Date.MonthName(_),
                            3
                        )
                    ),

                    // Número do mês
                    Date.Month(_)
                }
            )
        )

in
    CalendarTable
