# 🔹 Dimensão Calendário

📄 Referência: docs/05_modelagem.md

## 🎯 Objetivo

Criar dimensão temporal para suportar análises YoY, AH e AV.

---

## ⚙️ Implementação

```powerquery
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
```md
## 🧠 Observações

- Geração dinâmica baseada na tabela fato
- Suporte a análises temporais
- Essencial para cálculos DAX (YoY, AH)
