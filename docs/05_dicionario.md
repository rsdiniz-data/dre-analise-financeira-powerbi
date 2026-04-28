# 5. Dicionário de Dados
## 📘 5.1 Tabela `dPlanoConta`
## 5.1.1 Descrição

A tabela dPlanoConta é a dimensão responsável por estruturar a hierarquia do plano de contas da DRE.

Ela permite análises por níveis hierárquicos (Grupo, Subgrupo e Conta Analítica), garantindo navegação estruturada nos relatórios financeiros.

Além disso, contém a classificação contábil das contas e indicadores auxiliares utilizados na consolidação de métricas e indicadores financeiros no modelo analítico.

---

## 5.1.2 Estrutura
Coluna	Tipo de Dado	Descrição	Relacionamentos
ID Conta	Texto	Código identificador único da conta contábil	1:* → ftResultado[ID Conta]
Descrição	Texto	Nome ou descrição da conta contábil	—
Lançamento	Número inteiro	Define se a conta permite lançamentos (1 = analítica, 0 = sintética)	—
N1	Texto	Nível 1 — Grupo principal da DRE (ex.: Receita, Custos, Despesas)	—
N2	Texto	Nível 2 — Subgrupo contábil	—
N3	Texto	Nível 3 — Conta analítica	—
CodDRE	Texto	Código do grupo da DRE para consolidação de indicadores	—
Calculado	Número inteiro	Indicador auxiliar para controle de cálculos e agregações	—
TipoIndicador	Número inteiro	Classificação do tipo de indicador (Receita, Custo, Despesa, etc.)	—

---

## 5.1.3 Observações
A hierarquia é definida com base na estrutura do código da conta
Contas sintéticas (Lançamento = 0) são utilizadas apenas para agregação
A coluna TipoIndicador é utilizada para ajustar sinais e cálculos nas análises

---

## 📘 5.2 Tabela ftResultado
## 5.2.1 Descrição

A tabela ftResultado representa a tabela fato do modelo dimensional.

Ela armazena os valores financeiros da DRE por conta contábil e data, sendo a base para cálculos e indicadores financeiros.

---

## 5.2.2 Estrutura
Coluna	Tipo de Dado	Descrição	Relacionamentos
ID Conta	Texto	Código da conta contábil associado ao valor financeiro	*:1 → dPlanoConta[ID Conta]
Data	Data	Data de referência do valor (fechamento do exercício)	*:1 → dCalendario[Data]
Valor	Número decimal	Valor monetário registrado para a conta na data informada	—

---

## 5.2.3 Observações
Contém apenas contas analíticas (Lançamento = 1)
Os dados estão no formato long (unpivoted), permitindo análises temporais
Base para todos os KPIs e indicadores financeiros do modelo

---

## 📘 5.3 Tabela dCalendario
## 5.3.1 Descrição

A tabela dCalendario é a dimensão de tempo do modelo.

Ela garante continuidade de datas e permite análises temporais como comparações anuais (YoY), análise horizontal (AH) e vertical (AV).

---

## 5.3.2 Estrutura
Coluna	Tipo de Dado	Descrição	Relacionamentos
Data	Data	Data completa utilizada nas análises temporais	1:* → ftResultado[Data]
Ano	Número inteiro	Ano correspondente à data	—
Mes	Texto	Nome abreviado do mês (Jan, Fev, etc.)	—
Mes_Num	Número inteiro	Número do mês (1 a 12), utilizado para ordenação cronológica	—

---

## 5.3.3 Observações
A tabela cobre todo o intervalo de datas da tabela fato
A coluna Mes_Num deve ser utilizada para ordenação do campo Mes
Pode ser expandida com novos atributos (Trimestre, Semana, etc.)

---

## ⭐ 5.4 Estrutura Final do Modelo

O modelo segue o padrão dimensional Star Schema, com separação clara entre fato e dimensões:

dPlanoConta (1) → (*) ftResultado
dCalendario (1) → (*) ftResultado
💡 Considerações Finais

A estrutura adotada garante:

Organização e padronização dos dados
Facilidade na construção de métricas em DAX
Escalabilidade do modelo analítico
Suporte a análises financeiras complexas
