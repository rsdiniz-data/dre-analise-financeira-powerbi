# Power Query (ETL)

Este diretório contém os scripts responsáveis pelo processo de ingestão, transformação e carga dos dados.

## Estrutura

- transformacoes.md → pipeline completo de dados

## Etapas

1. Extração de dados de arquivos PDF
2. Transformação e limpeza
3. Construção da tabela fato (ftResultado)
4. Criação das dimensões (dPlanoConta, dCalendario)

## Referências

- docs/04_pipeline_dados.md
- docs/05_modelagem.md

## Observação

O processo segue abordagem de ETL dentro do Power BI, com foco em preparação para modelagem dimensional.

## Rastreabilidade

Cada script contém referências diretas às seções da documentação em /docs.
