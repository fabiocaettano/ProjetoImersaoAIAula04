# Projeto Imersao AI Aula 04

## Objetivo 
Criar um Chat Box para pesquisa climática dos últimos 7 dias conforme a cidade pesquisada.

## Fonte de Dados 
Utilizado uma API pública do Instituto Nacional de pesquisas espaciais o INPE.

## Como foi construido o Chat Box

### Pergunta 01 Goolge AI Studio: 

```

Com base em api pública, construir um dicionário na linguagem python, utilizando como referência  o endpoint http://servicos.cptec.inpe.br/XML/listaCidades?city=var_city , no endpoint foi informado "var_city" isto é uma variavel a ser informado por input antes de realizar a consulta no endpoint.
```

<p>Observação: O código apresentado já atendeu o que imaginei</p>

<p>Retorno ao executar o código:</p>

```
Digite o nome da cidade: sao paulo
Dicionário de cidades:
ID: 244, Nome: São Paulo, UF: SP
ID: 5019, Nome: São Paulo das Missões, UF: RS
ID: 5020, Nome: São Paulo de Olivença, UF: AM
ID: 5021, Nome: São Paulo do Potengi, UF: RN
```


### Pergunta 02 ao Google AI Studio:

<p>Logo após executar a instrução for, inserir um novo input solicitando o id da cidade</p>

<p>Observação: A ideia do codigo atendeu a expectativa, portém a biblioteca utlizada para execuar o parser no XML não exibia o resultado</p>

<p>Retorno ao executar o código: </p>

```

Digite o ID da cidade para mais informações: 1433
Previsão do tempo para os próximos 7 dias:
Data: 2024-05-12
Tempo: Parcialmente Nublado
Temperatura mínima: 23
Temperatura máxima: 31
--------------------------------------------
Data: 2024-05-13
Tempo: Chuvas Isoladas
Temperatura mínima: 23
Temperatura máxima: 32
--------------------------------------------
Data: 2024-05-14
Tempo: Parcialmente Nublado
Temperatura mínima: 23
Temperatura máxima: 32
--------------------------------------------
Data: 2024-05-15
Tempo: Chuvas Isoladas
Temperatura mínima: 23
Temperatura máxima: 32
--------------------------------------------
Data: 2024-05-16
Tempo: Chuvas Isoladas
Temperatura mínima: 23
Temperatura máxima: 33
--------------------------------------------
Data: 2024-05-17
Tempo: Chuva
Temperatura mínima: 24
Temperatura máxima: 30
```


## Adaptações no código python

### Parse no XMM

<p>No segundo input, o código python não retornava os resultados, exibia a chave mas não exibia o valor.</p>
<p>Como não tenho muito conhecimento em Python, fiz um pesquisa e substitui a biblioteca "xml.etree.ElementTree" pela "xml.etree.ElementTree". Adaptei o for sugerido anteriormente.</p>


### Tradução do sigla Tempo

<p>No retorno da consulta a chave tempo retorna uma flag.</p>
<p>No site do INEP, localizei uma tabela com chave e valor.</p>
<p>Importei esta tabela para o Google AI STUDIO e fiz a seguinte requisições:</p>
<p>Com base no arquivo importado, criar um dicionário na linguagem python.</p>
<p>O Google AI Studio retornou o solicitado.</p>
<p>E retornou com um exemplo para recuperar o valor da chave: description = weather_dict[abbreviation]</p>
<p>Colei o dicionário no código.</p>
<p>E dentro do for substituir o retorno da flag, pelo seu valor ficando melhor para visualizar a situação do clima:</p>
```
elif child.tag == "tempo":
  tempo = weather_dict[child.text]
```



