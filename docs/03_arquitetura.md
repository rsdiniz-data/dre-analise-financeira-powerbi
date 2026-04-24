# 3. Arquitetura da Solução

A solução foi construída com base em modelagem dimensional (Star Schema).

## 3.1 Tabela Fato

- ftResultado

## 3.2 Tabelas Dimensão

- dPlanoConta
- dCalendario

## 3.3 Relacionamentos

- dPlanoConta (1:N) → ftResultado  
- dCalendario (1:N) → ftResultado