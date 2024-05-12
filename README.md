# Projeto Imersao AI Aula 04

<p>Imersão na inteligência artificial no Gemini e a IA do Googe.</p>
<p></p>Realizada em 2024 pela a Alura e o Google.</p>
<p></p>Desafio, criar um projeto utilizando estas ferramentas.</p>


## 1.0 Projeto para participar do desafio
<p>Criar um Chat Box para pesquisa climática dos últimos 7 dias conforme a cidade pesquisada.</p>
<p>E solicitar análise desses dados oara inteligência artifical do Google</p>

## 2.0 Fonte de Dados 
<p>Utilizado uma API pública do Instituto Nacional de pesquisas espaciais o INPE.</p>

## 3.0 Como foi construido o Chat Box

### 3.1 Pergunta 01 Goolge AI Studio: 

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


### 3.2 Pergunta 02 ao Google AI Studio:

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


### 3.3 Adaptações no código python

### 3.3.1 Parse no XML

<p>No segundo input, o código python não retornava os resultados, exibia a chave mas não exibia o valor.</p>
<p>Como não tenho muito conhecimento em Python, fiz um pesquisa e substitui a biblioteca para "xml.etree.ElementTree". E adaptei o "for" sugerido anteriormente.</p>


### 3.3.2 Tradução do sigla Tempo

<p>No retorno da consulta a chave tempo retorna uma flag.</p>
<p>No site do INEP, localizei uma tabela com chave e valor, e criei um arquivo no formato xlsx.</p>
<p>Importei este arquivo para o Google AI STUDIO e fiz a seguinte pergunta:</p>

```
Com base no arquivo importado, criar um dicionário na linguagem python
```

<p>O Google AI Studio retornou o solicitado.</p>
<p>E retornou com um exemplo para recuperar o valor da chave: description = weather_dict[abbreviation]</p>
<p>Colei o dicionário no código.</p>
<p>E dentro do for substituir o retorno da flag, pelo seu valor ficando melhor para visualizar a situação do clima:</p>


```
elif child.tag == "tempo":
  tempo = weather_dict[child.text]
```


## 4.0 Como Funciona o CHATBOX

### Perguta 4.1
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

### 4.2 Perguta 2
<p>Agora o ChtaBox solicita o ID da cidade, pois na consulta pode retornar outras cidades</p>

```
Digite o ID da cidade para mais informações: 241
```

### 4.3 Analise do Gemini

<p>No código python foi montada um pergunta sobre clima, com base no dicionário previsoes</p>
<p>A variavel analise recebeu estas informações</p>
<p>E faz a seguinte pergunta ao modelo, que varia conforme a consulta:</p>

```
Gostaria de uma análise sobre a previsão do tempo conforme dados coletados no INPE : no dia 2024-05-12 com tempo Parcialmente Nublado e temperatura minima de 24 e temperatura máxima de 35; no dia 2024-05-13 com tempo Parcialmente Nublado e temperatura minima de 24 e temperatura máxima de 35; no dia 2024-05-14 com tempo Parcialmente Nublado e temperatura minima de 22 e temperatura máxima de 29; no dia 2024-05-15 com tempo Parcialmente Nublado e temperatura minima de 21 e temperatura máxima de 26; no dia 2024-05-16 com tempo Chuvas Isoladas e temperatura minima de 21 e temperatura máxima de 26; no dia 2024-05-17 com tempo Parcialmente Nublado e temperatura minima de 21 e temperatura máxima de 33; no dia 2024-05-18 com tempo Parcialmente Nublado e temperatura minima de 24 e temperatura máxima de 34;
```

Com a configuração abaixo o modelo é acionado:

```
GOOGLE_API_KEY=''      
genai.configure(api_key=GOOGLE_API_KEY)
model = genai.GenerativeModel('gemini-pro')
response = model.generate_content(analise)
print(response.text)
```


Resposta:
```
**Análise da Previsão do Tempo para 2024-05-12 a 2024-05-18**

**Tendências Gerais:**

* Predominância de tempo parcialmente nublado com intervalos de sol.
* Temperaturas estáveis, variando entre 21°C e 35°C.
* Expectativa de chuvas isoladas no dia 16 de maio.

**Previsão Diária:**

* **12/05/2024 (Domingo):** Parcialmente nublado, temperatura mínima de 24°C e máxima de 35°C.
* **13/05/2024 (Segunda-feira):** Parcialmente nublado, temperatura mínima de 24°C e máxima de 35°C.
* **14/05/2024 (Terça-feira):** Parcialmente nublado, temperatura mínima de 22°C e máxima de 29°C.
* **15/05/2024 (Quarta-feira):** Parcialmente nublado, temperatura mínima de 21°C e máxima de 26°C.
* **16/05/2024 (Quinta-feira):** Chuvas isoladas, temperatura mínima de 21°C e máxima de 26°C.
* **17/05/2024 (Sexta-feira):** Parcialmente nublado, temperatura mínima de 21°C e máxima de 33°C.
* **18/05/2024 (Sábado):** Parcialmente nublado, temperatura mínima de 24°C e máxima de 34°C.

**Observações:**

* As temperaturas noturnas devem ser amenas, enquanto as temperaturas diurnas devem ser agradáveis.
* O dia mais frio do período previsto é 15 de maio, com temperaturas máximas de 26°C.
* O dia mais quente do período previsto é 13 de maio, com temperaturas máximas de 35°C.
* A previsão é sujeita a alterações, especialmente com o passar do tempo.
```


## Conclusão

<p> Assustador como a ferramenta desenvolveu a ideia do ChatBox junto com a Lingaugem Python.</p>
<p> Com as instruções no prompt do Google IA Studiom e testes realizados no Google COLAB</p>
<p> Tenho conhecimento de desenvolvimento de sistemas, mas nenhum conhecimento avançado na linguagem Python.</p>
<p> E a Cereja do Bolo é o retorno da Inteligçencia Artificial do Google, avaliando os dados informados </p>
<p> Projeto concluido </p>.
