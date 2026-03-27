# power_bi_projetos
#Meus projetos build-to-learn de power bi! :)

Realizo os tratamentos e modelagens em sql e python, quando necessário.
Disponivel nos arquivos:
- codigos.py
- codigos.sql

Banco de dados utilizado no projeto:
- Supabase (PostgreSQL)

Etapa 1 - Download dos dados em csv

Os dados foram baixados do sistema PGA-SIGSIF oficial do Ministério da Agricultura e Pecuária(MAPA)
Abaixo os links:
https://sistemas.agricultura.gov.br/pga_sigsif/pages/view/sigsif/relatoriocomercializacao/index.xhtml
https://sistemas.agricultura.gov.br/pga_sigsif/pages/view/sigsif/relatorioproducao/index.xhtml

Os arquivos foram baixados em csv.

Etapa 2 - ETL para tratamento dos dados em Python(pandas) e carregamento no banco de dados do Supabase(PostgreSQL)

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

Etapa 3 - SQL para modelagem e enriquecimento de dados epara elaboração das views que serão usadas no PowerBI

Produção
- 

Comércio Nacional
- 

Comércio Internacional
- 

Códigos em:
- producao.sql
- comercio_nacional.sql
- comercio_internacional.sql


## Dicionarios de dados no PowerBI (OutPut)

### Dicionário de Dados: Tabela Fato `sif_producao_bovino`

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `data` | Date | Data considerando mês e ano da produção |
| `uf` | String | Estado da localização da produção |
| `produto` | String | Produto produzido |
| `total_produzido`| NUMERIC(21, 3)| Quantidade produzida |
| `ossos`| String| Presença de ossos sendo "Com osso" e "Sem osso" |
| `temperatura`| String | Temperatura do produto sendo "Congelado", "Resfriado" e "Ambiente" |


### Dicionário de Dados: Tabela Fato `sif_comercio_internacional_bovino`

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `data` | Date | Data considerando mês e ano da produção |
| `uf` | String | Estado da localização da produção |
| `produto` | String | Produto produzido |
| `total_produzido`| NUMERIC(21, 3)| Quantidade produzida |
| `ossos`| String| Presença de ossos sendo "Com osso" e "Sem osso" |
| `temperatura`| String | Temperatura do produto sendo "Congelado", "Resfriado" e "Ambiente" |


### Dicionário de Dados: Tabela Fato `sif_comercio_nacional_bovino`

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `data` | Date | Data considerando mês e ano da produção |
| `uf` | String | Estado da localização da produção |
| `produto` | String | Produto produzido |
| `total_produzido`| NUMERIC(21, 3)| Quantidade produzida |
| `ossos`| String| Presença de ossos sendo "Com osso" e "Sem osso" |
| `temperatura`| String | Temperatura do produto sendo "Congelado", "Resfriado" e "Ambiente" |


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


