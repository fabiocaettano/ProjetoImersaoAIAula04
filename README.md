# Projeto Imersao AI Aula 04

## Objetivo 
Criar um Chat Box para pesquisa climática dos últimos 7 dias conforme a cidade pesquisada.

## Fonte de Dados 
Utilizado API pública do Instituto Nacional de pesquisas espaciais o INPE.

## Como foi construido o Chat Box

<b>Pergunta 01 Goolge AI Studio: </b>
Com base em api pública, construir um dicionário na linguagem python, utilizando como referência  o endpoint http://servicos.cptec.inpe.br/XML/listaCidades?city=var_city , no endpoint foi informado "var_city" isto é uma variavel a ser informado por input antes de realizar a consulta no endpoint.

Observação: O código apresentado já atendeu o que imaginei

Retorno ao executar o código:
```
Digite o nome da cidade: sao paulo
Dicionário de cidades:
ID: 244, Nome: São Paulo, UF: SP
ID: 5019, Nome: São Paulo das Missões, UF: RS
ID: 5020, Nome: São Paulo de Olivença, UF: AM
ID: 5021, Nome: São Paulo do Potengi, UF: RN
```

<b>Pergunta 02 ao Google AI Studio:</b2>
Logo após executar a instrução for, inserir um novo input solicitando o id da cidade

## Adaptações no código python
