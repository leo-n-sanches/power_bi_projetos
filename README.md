# Projeto de pesquisa macroeconômica do mercado de carnes SIF.
## Meu projeto build-to-learn de Python, SQL e PowerBI! :)

## Objetivos

- Identificar quais estados são os maiores produtores e compradores de cada um dos produtos selecionados.
- Quais paises são importadores dos produtos selecionados, com suas preferencias e sazonalidades.
- Quais métricas de produtos tem maior influencia em cada estado ou papis (congelado/resfriado) e (com osso / sem osso).
- Recortes de faixas de periodo de datas, identificar sazonalidades e acumulados total, por ano e por mês.

## Aplicação em negócio

- Varejo e atacado identificar oportunidades para compra desses produtos, por estado, periodo e métricas avaliadas, expandindo carteira de fornecedores e reduzindo custos.
- Frigorificos ao identificar estados que não possuem produção própria podem criar estratégias de vendas para expandir distribuição e lucro.
- Fazendas ao identificar sazonalidades, podem tentar vender seus rebanhos para estados com menor produção a um preço maior, além de identificar os melhores periodos para venda, com maior consumo e menor produção e disponibilidade. 
- Frigorificos podem calcular métricas para identificar seu market share nacional, internacional, e de produção, seu crescimento e suas tendencias.
- Frigorificos, exportadoras brasileiras e importadoras estrangeiras podem identificar sazonalidades, preferencias, volume de comercialização e tendencias para elaborar estratégias de vendas para paises estrangeiros.
- Frigorificos podem identificar estados que terceirizam suas produções.

## Requisitos

- Extração de dados públicos do site oficial do SIF
- Banco de dados para armazenamento dos dados
- URL e API KEY para conexão do Python ao banco de dados
- URL e permissão para conexão do banco de dados ao PowerBI

## Resultado esperado

3 Dashboards com filtros e apresentação preparados com todas as informações relevantes para tomada de decisão.

## Techstack
- SQL (postgresql)
- Python (pandas)
- PowerBI

### Banco de dados utilizado no projeto:
- Supabase (PostgreSQL)

## Etapa 1 - Download dos dados em csv

Os dados foram baixados do sistema PGA-SIGSIF oficial do Ministério da Agricultura e Pecuária(MAPA)
Abaixo os links:
https://sistemas.agricultura.gov.br/pga_sigsif/pages/view/sigsif/relatoriocomercializacao/index.xhtml
https://sistemas.agricultura.gov.br/pga_sigsif/pages/view/sigsif/relatorioproducao/index.xhtml

Os arquivos foram baixados em csv.

## Etapa 2 - ETL para tratamento dos dados em Python(pandas) e carregamento no banco de dados do Supabase(PostgreSQL)

Os dados foram carregados no VScode e então foram realizados os tratamentos de:
- Carregamento dos csv e criação dos dataframes
- Coleta de informações para criação dos dicionários de dados
- Correção de nomes de colunas
- Correção de datas
- Correção de tipos
- Preenchimento de NaN
- Criação de coluna "id" que será a "pk" no banco de dados
- Conexão com o banco de dados por API KEY
- Envio de arquivos para o banco de dados

Simultaneamente a isso foram realizados no banco de dados:
- Criação das tabelas silver com nomes corretos das colunas
- Definição dos tipos corretos de cada coluna

Informações em:
- codigo_etl.py
- codigo_etl.sql

## Etapa 3 - SQL para modelagem e enriquecimento de dados epara elaboração das views que serão usadas no PowerBI

Total de produtos distintos na base (População) = 274
Total de produtos escolhidos para análise (Amostra) = 4
Sendo eles:
- 'CARNE RESFRIADA DE BOVINO COM OSSO'
- 'CARNE RESFRIADA DE BOVINO SEM OSSO'
- 'CARNE CONGELADA DE BOVINO SEM OSSO'
- 'CARNE CONGELADA DE BOVINO COM OSSO'

Sendo criadas 2 métricas:
- Com osso / Sem osso
- Congelada / Resfriada

Querys:
- CTE para enriquecimento de dados e criação de métricas
- Criação de tabela schema gold para organização de dados enriquecidos e tratados
- Seleção de produtos e colunas que serão utilizados para criação dos dashboards
- Criação de view para conectar ao PowerBI

Códigos em:
- producao.sql
- comercio_nacional.sql
- comercio_internacional.sql

## Etapa 4 - Estruturação de dashboards e apresentação em PowerBI

Criação das dimensões de calendário e geográfico para mapas
Criação de medidas e organização em pastas
Criação de um Top 3 em cada dashboard
Utilização do 3-30-300 para melhorar o fluxo de visualização do dashboards pelo tomador de decisão
Tooltips para enriquecer as informações durante a navegação
Criação de filtro expansivel por botão
Navegação por dashboards utilizando botões
Criação de medidas de: YoY, % to total, % de variação do total, volume do total, volume de diferença do total
Dashboard estratégico de volume por ano, por mês e acumulado por mês para identificar sazonalidade mensal
Tabela de matriz para navegação detalhada pelos dados.
Tabela de mapa para visualização de paises que realizam a compra e seus volumes
Gráfico de barras(horizontal) para identificar e visualizar volumes e diferenças entre estados ou paises.

## Dicionarios de dados no PowerBI (OutPut)

### Dicionário de Dados: Tabela Fato `sif_producao_bovino`

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `data` | Date | Data considerando mês e ano |
| `uf` | String | Estado da localização da produção |
| `produto` | String | Produto produzido |
| `total_produzido`| NUMERIC(21, 3)| Quantidade produzida |
| `ossos`| String| Presença de ossos sendo "Com osso" e "Sem osso" |
| `temperatura`| String | Temperatura do produto sendo "Congelado" e "Resfriado" |

### Dicionário de Dados: Tabela Fato `sif_comercio_nacional_bovino`

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `data` | Date | Data considerando mês e ano |
| `uf_destino` | String | Estado destino da comercialização |
| `produto` | String | Produto comercializado |
| `qtd_comercializacao`| NUMERIC(21, 3)| Quantidade comercializada |
| `operador`| String | Comercialização realizada para estados ou para estabelecimentos SIF |
| `ossos`| String| Presença de ossos sendo "Com osso" e "Sem osso" |
| `temperatura`| String | Temperatura do produto sendo "Congelado" e "Resfriado" |

### Dicionário de Dados: Tabela Fato `sif_comercio_internacional_bovino`

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `data` | Date | Data considerando mês e ano |
| `pais_destino` | String | País destino da comercialização |
| `produto` | String | Produto comercializado |
| `qtd_comercializacao`| NUMERIC(21, 3)| Quantidade comercializada |
| `ossos`| String| Presença de ossos sendo "Com osso" e "Sem osso" |
| `temperatura`| String | Temperatura do produto sendo "Congelado" e "Resfriado" |

### Dicionário de Dados: Tabela Dimensão `dim_calendario_br`

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `pais` | String | Nome do pais (Brasil) |
| `uf` | String | Nome do estado |
| `nome_uf` | String | Sigla do estado |
| `regiao`| String | Região do país |
| `nome_uf_mapa_formas`| String | Nome do estado sem acentos, para mapa de formas PowerBI |

### Dicionário de Dados: Tabela Dimensão `dim_estados`

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `data_id` | Int64 | ID |
| `data` | String | Data por extenso |
| `ano` | Int64 | Número do ano |
| `trimestre`| Int64 | Número do trimeste |
| `mes`| Int64 | Número do mês |
| `nome_mes`| String | Nome do mês |
| `semana_ano`| Int64 | Número da semana do ano |
| `dia_semana`| Int64 | Número do dia da semana |
| `nome_dia`| String | Nome do dia da semana |
| `is_final_semana`| Boolean | Se é final de semana ou não |


