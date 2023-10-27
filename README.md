# Pesquisa Origem Destino

Bases de dados Origem

https://transparencia.metrosp.com.br/dataset/pesquisa-origem-e-destino


1977

Base ok, inclusive com municípios

## 1987

Base ok, inclusive com municípios

## 1997

Base ok, inclusive com zonas e municípios

## 2007

Base ok, inclusive com zonas e municípios

## 2017

Base 2017 ok, inclusive com zonas e municípios

## Projeções da População - IBGE

Projeções da população por sexo e idades (xls | ods) - atualizado em 06/04/2020

https://www.ibge.gov.br/estatisticas/sociais/populacao/9109-projecao-da-populacao.html

Arquivo usado para elaborarmos a projeção da população de acordo com a faixa etária para a base de 2017.

[projecoes_2018_populacao_2010_2060_20200406.xls](projecoes_2018_populacao_2010_2060_20200406.xls)

Script para tratamento dos dados e inclusão de informações sobre projeção IBGE [OD_2017_tratamento_inclusao_projecao_IBGE](OD_2017_tratamento_inclusao_projecao_IBGE).

O dataframe de saída conterá as colunas abaixo:

'ID_PESS',           'IDADE',    'GRUPO ETÁRIO',
                    2017,              2018,              2019,
                    2020,              2021,              2022,
                    2023,              2024,              2025,
                    2026,              2027,              2028,
                    2029,              2030,              2031,
                    2032,              2033,              2034,
                    2035,              2036,              2037,
                    2038,              2039,              2040,
                    2041,              2042,              2043,
                    2044,              2045,              2046,
                    2047,              2048,              2049,
                    2050,              2051,              2052,
                    2053,              2054,              2055,
                    2056,              2057,              2058,
                    2059,              2060, 'FATOR_2017_2023',
       'FATOR_2017_2025', 'FATOR_2017_2035', 'FATOR_2017_2040',
       'FATOR_2017_2045', 'FATOR_2017_2050', 'FATOR_2017_2055',
       'FATOR_2017_2060'

O campo ID_PESS será usado para "ligar" com a base de dados do Power BI, e os campos "FATOR_2017_YYYY" são as colunas
que geram um fator de comparação entre a projeção do IBGE de 2017 e o ano final do nome da coluna, por exemplo,
a coluna FATOR_2017_2025 compara o fator de evolução daquele grupo de 2017 até 2025.

O arquivo de saída está disponível no caminho [OD_2017_fator_de_comparação_IBGE.xlsx](OD_2017_fator_de_comparação_IBGE.xlsx).

### Faixas etárias

A partir da coluna IDADE da base OD_2017 foi possível criar o mesmo grupo etário do IBGE, que foi utilizado para fazer o "merge" entre as duas bases de dados (Base OD2017 e Base IBGE).

O código para criar a coluna da faixa etária na base OD_2017 está descrita abaixo:

```py
# a partir dos grupos etários da lista do ibge, cria a coluna 
# grupo_etario no dataframe OD2017, incluindo o seu grupo etário
grupos = [
    0,
    4,
    9,
    14,
    19,
    24,
    29,
    34,
    39,
    44,
    49,
    54,
    59,
    64,
    69,
    74,
    79,
    84,
    89,
    150
]
labels = df_faixas_etarias['grupo_etario'].to_list()
df['grupo_etario'] = pd.cut(
    df['IDADE - Idade'],
    bins=grupos,
    include_lowest=False,
    precision=0,
    labels=labels
)
df[['IDADE - Idade', 'grupo_etario']].tail()
```
