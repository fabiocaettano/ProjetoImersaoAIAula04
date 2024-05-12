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


<p>Retorno ao executar o código:</p>

```
Digite o nome da cidade: sao paulo
Dicionário de cidades:
ID: 244, Nome: São Paulo, UF: SP
ID: 5019, Nome: São Paulo das Missões, UF: RS
ID: 5020, Nome: São Paulo de Olivença, UF: AM
ID: 5021, Nome: São Paulo do Potengi, UF: RN
```

<p>O código apresentado para pergunta 1 já atendeu o esperado.</p>


### Pergunta 02 ao Google AI Studio:

```
Logo após executar a instrução for, inserir um novo input solicitando o id da cidade
```

<p>Retorno ao executar o código: </p>

```

Digite o ID da cidade para mais informações: 1433
Previsão do tempo para os próximos 7 dias:
Data: 
Tempo: 
Temperatura mínima: 
Temperatura máxima:
```

<p>Observação: A ideia do codigo atendeu a expectativa, portém a biblioteca utlizada para execuar o parser no XML não exibia o resultado</p>


## Adaptações no código python

### Parse no XML

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


## Como Funciona o CHATBOX

<p>O CHATBOX faz uma pergunta sobre a cidade, o usuário deverá informar sem acentos</p>

```

Digite o nome da cidade: rio de janeiro
```

<p>Ao informar o nome da cidade, envia a consulta para API e retorna com a seguinte informação:</p>

```

Dados climáticos:
Cidade: Rio de Janeiro
Estado: RJ
ID: 241
```

<p>Agora o ChtaBox solicita o ID da cidade, pois na consulta pode retornar outras cidades></p>

```
Digite o ID da cidade para mais informações: 241
```

<p>Faz a segunda consulta em outro endpoint:</p>

```

Previsão do tempo para os próximos 7 dias:
Data: 2024-05-12
Tempo: Parcialmente Nublado
Temperatura mínima: 23
Temperatura máxima: 33
--------------------------------------------
Data: 2024-05-13
Tempo: Parcialmente Nublado
Temperatura mínima: 24
Temperatura máxima: 34
--------------------------------------------
Data: 2024-05-14
Tempo: Parcialmente Nublado
Temperatura mínima: 22
Temperatura máxima: 29
--------------------------------------------
Data: 2024-05-15
Tempo: Parcialmente Nublado
Temperatura mínima: 21
Temperatura máxima: 27
--------------------------------------------
Data: 2024-05-16
Tempo: Parcialmente Nublado
Temperatura mínima: 21
Temperatura máxima: 28
--------------------------------------------
Data: 2024-05-17
Tempo: Parcialmente Nublado
Temperatura mínima: 22
Temperatura máxima: 32
--------------------------------------------
```
