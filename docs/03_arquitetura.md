# 3. Arquitetura da Solução

A solução foi construída com base em modelagem dimensional (Star Schema), com o objetivo de otimizar a performance das análises e garantir escalabilidade do modelo.

Essa abordagem permite separar claramente os dados transacionais (fato) das estruturas analíticas (dimensões), facilitando a criação de métricas e a navegação nos dados.

## 3.1 Tabela Fato

- **ftResultado**  
  Armazena os valores financeiros da DRE ao longo do tempo, representando os eventos mensuráveis do negócio.

## 3.2 Tabelas Dimensão

- **dPlanoConta**  
  Responsável pela estrutura hierárquica da DRE (níveis N1, N2, N3), classificação das contas e definição dos indicadores.

- **dCalendario**  
  Permite análises temporais, como evolução histórica, comparações YoY e agregações por período.

## 3.3 Relacionamentos

- dPlanoConta (1:N) → ftResultado  
- dCalendario (1:N) → ftResultado  

Esses relacionamentos garantem a integridade do modelo e possibilitam análises multidimensionais de forma eficiente.
