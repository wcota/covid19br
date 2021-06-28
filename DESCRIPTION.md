DOI para citação: 10.1590/SciELOPreprints.362

Mais informações: [README.en.md](README.en.md)

[**DESCRIPTION in English**](DESCRIPTION.en.md)

# Descrição dos dados e utilização

Em geral, os arquivos estão no formato CSV, um formato livre e aberto de fácil acesso. Os nomes dos arquivos podem não ser os ideais, mas foram mantidos para não quebrar a compatibilidade de acesso por pessoas que já usavam os nomes antigos.

Exemplo de acesso aos dados com `pandas` no Python: <https://colab.research.google.com/drive/1H1N387IIAGV-3YRtyxzPz94vSiLrhE0M?usp=sharing>

## Definição de nomes e referências

| nome     | descrição                                       | url                                             |
|----------|-------------------------------------------------|-------------------------------------------------|
| CC BY    | Licença Creative Commons CC BY 4.0              | https://creativecommons.org/licenses/by/4.0/    |
| CC BY-SA | Licença Creative Commons CC BY-SA 4.0           | https://creativecommons.org/licenses/by-sa/4.0/ |
| MS       | Ministério da Saúde                             | https://covid.saude.gov.br/                     |
| IBGE     | Instituto Brasileiro de Geografia e Estatística | https://www.ibge.gov.br/                        |
| SES      | Secretarias Estaduais de Saúde                  | Diversos                                        |
| BrIO     | Brasil.IO                                       | https://brasil.io/covid19/                      |
| Bra1     | @coronavirusbra1                                | https://coronavirusbra1.github.io/              |
| Gi       | GISCARD                                         | http://www.giscard.com.br/coronavirus           |
| OSM      | OpenStreetMap                                   | https://www.openstreetmap.org/                  |

## Coluna `epi_week`

Essa coluna corresponde ao número da semana epidemiológica. Ela vai de 1 até 53 para o ano de 2020. Em 2021, os números vão de 101 até 152. O primeiro dígito é utilizado para indicar que corresponde ao ano de 2021.
Para obter a semana epidemiológica bruta, utilize a [operação módulo](https://pt.wikipedia.org/wiki/Opera%C3%A7%C3%A3o_m%C3%B3dulo). Por exemplo, no Python:

```python
semana_epidemiologica = 152 % 100 # = 52
```

Os intervalos são definidos pelo Ministério da Saúde no Calendário Epidemiológico:

- 2020: http://portalsinan.saude.gov.br/calendario-epidemiologico-2020
- 2021: http://www.portalsinan.saude.gov.br/calendario-epidemiologico

## Arquivos com dados de COVID-19

Esses são os arquivos com os dados principais. Os arquivos `cases-brazil-states.csv` e `cases-brazil-total.csv` possuem dados em nível de unidades federativas, apenas. Já `cases-brazil-cities*.csv` possuem dados em nível municipal. 

Todas métricas por 100 mil habitantes são calculadas dividindo o número pela população e multiplicando por 10⁵; veja `cities_info.csv`.

### Por unidade federativa: `cases-brazil-total.csv` e `cases-brazil-states.csv`

Os dois arquivos possuem colunas iguais. A linha do tempo completa está disponível em `cases-brazil-states.csv`, enquanto `cases-brazil-total.csv` possui os números do último registro.

| nome                                   | descrição                                                             | fontes     | licença         |
|----------------------------------------|-----------------------------------------------------------------------|------------|-----------------|
| epi_week                               | Número da semana epidemiológica                                       | MS         |                 |
| date                                   | Data de divulgação                                                    |            |                 |
| country                                | Nome do país (sempre `Brazil`)                                        |            |                 |
| state                                  | Nome da unidade federativa                                            | IBGE       |                 |
| city                                   | Sempre “TOTAL”                                                        |            |                 |
| newDeaths                              | Número de novos óbitos divulgados                                     | MS,BrIO,Gi | CC BY, CC BY-SA |
| deaths                                 | Número acumulado de óbitos                                            | MS,BrIO,Gi | CC BY, CC BY-SA |
| newCases                               | Número de novos casos divulgados                                      | MS,BrIO,Gi | CC BY, CC BY-SA |
| totalCases                             | Número acumulado de casos                                             | MS,BrIO,Gi | CC BY, CC BY-SA |
| deathsMS                               | Número acumulado de obitos pelo Ministério da Saúde                   | MS         | CC BY           |
| totalCasesMS                           | Número acumulado de casos pelo Ministério da Saúde                    | MS         | CC BY           |
| deaths_per_100k_inhabitants            | Número de óbitos por 100 mil habitantes                               |            | CC BY           |
| totalCases_per_100k_inhabitants        | Número de casos por 100 mil habitantes                                |            | CC BY           |
| deaths_by_totalCases                   | Razão entre número de óbitos e casos (`deaths`/`totalCases`)          |            | CC BY           |
| recovered                              | Número de recuperados                                                 | Bra1,Gi    | CC BY           |
| suspects                               | Número de suspeitos                                                   | Bra1       | CC BY           |
| tests                                  | Número de testes realizados                                           | Bra1,Gi    | CC BY           |
| tests_per_100k_inhabitants             | Número de testes realizados por 100 mil habitantes                    |            | CC BY           |
| vaccinated                             | Número de pessoas que receberam a primeira dose                       | Bra1       | CC BY           |
| vaccinated_per_100_inhabitants         | Porcentagem de pessoas que receberam a primeira dose                  |            | CC BY           |
| vaccinated_second                      | Número de pessoas que receberam a segunda dose                        | Bra1       | CC BY           |
| vaccinated_second_per_100_inhabitants  | Porcentagem de pessoas que receberam a segunda dose                   |            | CC BY           |
| vaccinated_single                      | Número de pessoas que receberam a dose única                          | Bra1       | CC BY           |
| vaccinated_single_per_100_inhabitants  | Porcentagem de pessoas que receberam a dose única                     |            | CC BY           |

### Por municípios: `cases-brazil-cities.csv`, `cases-brazil-cities-time.csv.gz` e `cases-brazil-cities-time_changesOnly.csv`

Todos os arquivos possuem colunas iguais. Não há a coluna `epi_week` em `cases-brazil-cities.csv`. Não há as colunas `cod_RegiaoDeSaude` e `name_RegiaoDeSaude` em `cases-brazil-cities-time.csv.gz` e `cases-brazil-cities-time_changesOnly.csv`.

A linha do tempo completa está em `cases-brazil-cities-time.csv.gz` (compactação gzip), e os dados do último dia em `cases-brazil-cities.csv`. O arquivo `cases-brazil-cities-time_changesOnly.csv` é um subconjunto de `cases-brazil-cities-time.csv`, onde as colunas `newCases` e/ou `newDeaths` são não nulas.

| nome                            | descrição                                                    | fontes  | licença         |
|---------------------------------|--------------------------------------------------------------|---------|-----------------|
| epi_week                        | Número da semana epidemiológica                              | MS      |                 |
| date                            | Data de divulgação                                           |         |                 |
| country                         | Nome do país (sempre `Brazil`)                               |         |                 |
| state                           | Nome da unidade federativa                                   | IBGE    |                 |
| city                            | Nome do município                                            | IBGE    |                 |
| ibgeID                          | Código IBGE do município                                     | IBGE    |                 |
| newDeaths                       | Número de novos óbitos divulgados                            | MS,BrIO | CC BY, CC BY-SA |
| deaths                          | Número acumulado de óbitos                                   | MS,BrIO | CC BY, CC BY-SA |
| newCases                        | Número de novos casos divulgados                             | MS,BrIO | CC BY, CC BY-SA |
| totalCases                      | Número acumulado de casos                                    | MS,BrIO | CC BY, CC BY-SA |
| deaths_per_100k_inhabitants     | Número de óbitos por 100 mil habitantes                      |         | CC BY           |
| totalCases_per_100k_inhabitants | Número de casos por 100 mil habitantes                       |         | CC BY           |
| deaths_by_totalCases            | Razão entre número de óbitos e casos (`deaths`/`totalCases`) |         | CC BY           |
| _source                         | Fonte do dado: pode ser MS ou SES (via Brasil.IO)            |         |                 |
| last_info_date                  | Data de divulgação do último boletim da unidade federativa   | MS,BrIO | CC BY, CC BY-SA |
| cod_RegiaoDeSaude               | Código identificador da região de saúde do municipio         |         | CC BY           |
| name_RegiaoDeSaude              | Nome da região de saúde do município                         |         | CC BY           |

## Arquivos auxiliares

### Dados de cada município: `cities_info.csv`

| nome               | descrição                                                                    | fontes | licença |
|--------------------|------------------------------------------------------------------------------|--------|---------|
| ibge               | Código IBGE do município                                                     | IBGE   |         |
| city               | Nome do município                                                            | IBGE   |         |
| state              | Nome da unidade federativa                                                   | IBGE   |         |
| region             | Nome da região                                                               | IBGE   |         |
| pop2019            | Estimativa da população em 2019                                              | IBGE   |         |
| pop2020            | Estimativa da população em 2020                                              | IBGE   |         |
| isCountryside      | Igual a `1` se está no interior do Brasil, ou `0` se em região metropolitana | IBGE   |         |
| cod_RegiaoDeSaude  | Código identificador da região de saúde do municipio                         |        |         |
| name_RegiaoDeSaude | Nome da região de saúde do município                                         |        |         |

### Coordenadas GPS de cada município: `gps_cities.csv`

| nome     | descrição                | fontes | licença  |
|----------|--------------------------|--------|----------|
| ibgeID   | Código IBGE do município | IBGE   |          |
| id       | Nome do município        | IBGE   |          |
| lat      | Latitude                 | OSM    | ODbL 1.0 |
| lon      | Longitude                | OSM    | ODbL 1.0 |
| longName | Nome longo do município  | OSM    | ODbL 1.0 |

## Arquivos extras

- `_control.csv`: contém o último número de óbitos (deve ser deletado em algum momento)
- `_fixes_meta.csv`: correções nos registros do Ministério da Saúde
- `_tests_meta.csv`: metadados sobre os números de testes, por data e unidade federativa
- `sources.csv`: fontes dos dados
- `gps_cities.csv`: casos e óbitos por município, junto com as coordenadas GPS.
