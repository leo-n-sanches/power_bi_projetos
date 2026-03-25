# power_bi_projetos
#Meus projetos build-to-learn de power bi! :)

Realizo os tratamentos e modelagens em sql e python, quando necessário.
Disponivel nos arquivos:
- codigos.py
- codigos.sql

Banco de dados utilizado no projeto:
- Supabase (PostgreSQL)





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


