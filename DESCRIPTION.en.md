Current DOI: 10.1590/SciELOPreprints.362

More information: [README.en.md](README.md)

[**DESCRIPTION em português**](DESCRIPTION.md)

# Data description and usage

In general, the files are in CSV format.

Example with `pandas` on Python: <https://colab.research.google.com/drive/1H1N387IIAGV-3YRtyxzPz94vSiLrhE0M?usp=sharing>

## Name and reference definitions

| nome     | descrição                                       | url                                             |
|----------|-------------------------------------------------|-------------------------------------------------|
| CC BY    | Creative Commons CC BY 4.0 License              | https://creativecommons.org/licenses/by/4.0/    |
| CC BY-SA | Creative Commons CC BY-SA 4.0 License           | https://creativecommons.org/licenses/by-sa/4.0/ |
| MS       | Ministério da Saúde                             | https://covid.saude.gov.br/                     |
| IBGE     | Instituto Brasileiro de Geografia e Estatística | https://www.ibge.gov.br/                        |
| SES      | Secretarias Estaduais de Saúde                  |                                                 |
| BrIO     | Brasil.IO                                       | https://brasil.io/covid19/                      |
| Bra1     | @coronavirusbra1                                | https://coronavirusbra1.github.io/              |
| Gi       | GISCARD                                         | http://www.giscard.com.br/coronavirus           |
| OSM      | OpenStreetMap                                   | https://www.openstreetmap.org/                  |

## `epi_week` column

This column corresponds to the number of the epidemiological week. The values range from 1 to 53 in 2020, and from 101 to 152 in 2021. The first digit (1, for example) is used to indicate that this corresponds to the year 2021, instead of 2020. To obtain the respective epidemiological week, please use the [modulo operation](https://en.wikipedia.org/wiki/Modulo_operation). For example, using Python:

```python
epidemiological_week = 152 % 100 # = 52
```

The date intervals are defined by the Ministério da Saúde in their Epidemiological Calendar:

- 2020: http://portalsinan.saude.gov.br/calendario-epidemiologico-2020
- 2021: http://www.portalsinan.saude.gov.br/calendario-epidemiologico

## Dataset files of COVID-19 in Brazil

These are the main files of the dataset. The files `cases-brazil-states.csv` and `cases-brazil-total.csv` have data only at the federative units level. The files `cases-brazil-cities*.csv` have data at the municipality level.

All values by 100k inhabitants are evaluated dividing the number by population and multiplying by 10⁵; see `cities_info.csv`.

### By federative units: `cases-brazil-total.csv` and `cases-brazil-states.csv`

Both files share column names. The complete timeline is available at `cases-brazil-states.csv`, while `cases-brazil-total.csv` has only numbers for the last day.

| name                                   | description                                                       | sources    | license         |
|----------------------------------------|-------------------------------------------------------------------|------------|-----------------|
| epi_week                               | Epidemiological week                                              | MS         |                 |
| date                                   | Report date                                                       |            |                 |
| country                                | Name of the country (always `Brazil`)                             |            |                 |
| state                                  | Name of the federative unit                                       | IBGE       |                 |
| city                                   | Always “TOTAL”                                                    |            |                 |
| newDeaths                              | Number of reported new deaths                                     | MS,BrIO,Gi | CC BY, CC BY-SA |
| deaths                                 | Total number of deaths                                            | MS,BrIO,Gi | CC BY, CC BY-SA |
| newCases                               | Number of reported new cases                                      | MS,BrIO,Gi | CC BY, CC BY-SA |
| totalCases                             | Total number of cases                                             | MS,BrIO,Gi | CC BY, CC BY-SA |
| deathsMS                               | Total number of deaths by Ministério da Saúde                     | MS         | CC BY           |
| totalCasesMS                           | Total number of cases by Ministério da Saúde                      | MS         | CC BY           |
| deaths_per_100k_inhabitants            | Total number of deaths by 100k inhabitants                        |            | CC BY           |
| totalCases_per_100k_inhabitants        | Total number of cases by 100k inhabitants                         |            | CC BY           |
| deaths_by_totalCases                   | Fraction of deaths (`deaths`/`totalCases`)                        |            | CC BY           |
| recovered                              | Total number of recovered                                         | Bra1,Gi    | CC BY           |
| suspects                               | Total number of suspects                                          | Bra1       | CC BY           |
| tests                                  | Total number of tests                                             | Bra1,Gi    | CC BY           |
| tests_per_100k_inhabitants             | Total number of tests by 100k inhabitants                         |            | CC BY           |
| vaccinated                             | Total number of vaccinated with a first dose                      | Bra1       | CC BY           |
| vaccinated_per_100_inhabitants         | Percentage of vaccinated with a first dose                        |            | CC BY           |
| vaccinated_second                      | Total number of vaccinated with a second dose                     | Bra1       | CC BY           |
| vaccinated_second_per_100_inhabitants  | Percentage of vaccinated with a second dose                       |            | CC BY           |
| vaccinated_single                      | Total number of vaccinated with a single-shot                     | Bra1       | CC BY           |
| vaccinated_single_per_100_inhabitants  | Percentage of vaccinated with a single-shot                       |            | CC BY           |
| vaccinated_third                       | Total number of vaccinated with a booster shot                    | Bra1       | CC BY           |
| vaccinated_third_per_100_inhabitants   | Percentage of vaccinated with a booster shot                      |            | CC BY           |

### By municipalities: `cases-brazil-cities.csv`, `cases-brazil-cities-time.csv.gz` and `cases-brazil-cities-time_changesOnly.csv`

All files share column names. `epi_week` is not available in `cases-brazil-cities.csv`. The columns `cod_RegiaoDeSaude` and `name_RegiaoDeSaude` are not shown in `cases-brazil-cities-time.csv.gz` and `cases-brazil-cities-time_changesOnly.csv`.

The full timeline is available in `cases-brazil-cities-time.csv.gz` (with gzip compression, without columns `country`, `_source`, `last_info_date`), and data for the last day in `cases-brazil-cities.csv`. The file `cases-brazil-cities-time_changesOnly.csv` is a subset of `cases-brazil-cities-time.csv`, where `newCases` and/or `newDeaths` are non zero.

| name                            | description                                             | sources | license         |
|---------------------------------|---------------------------------------------------------|---------|-----------------|
| epi_week                        | Epidemiological week                                    | MS      |                 |
| date                            | Report date                                             |         |                 |
| country                         | Name of the country (always `Brazil`)                   |         |                 |
| state                           | Name of the federative unit                             | IBGE    |                 |
| city                            | Name of the municipality                                | IBGE    |                 |
| ibgeID                          | IBGE code of the municipality                           | IBGE    |                 |
| newDeaths                       | Number of reported new deaths                           | MS,BrIO | CC BY, CC BY-SA |
| deaths                          | Total number of deaths                                  | MS,BrIO | CC BY, CC BY-SA |
| newCases                        | Number of reported new cases                            | MS,BrIO | CC BY, CC BY-SA |
| totalCases                      | Total number of cases                                   | MS,BrIO | CC BY, CC BY-SA |
| deaths_per_100k_inhabitants     | Total number of deaths by 100k inhabitants              |         | CC BY           |
| totalCases_per_100k_inhabitants | Total number of cases by 100k inhabitants               |         | CC BY           |
| deaths_by_totalCases            | Fraction of deaths (`deaths`/`totalCases`)              |         | CC BY           |
| _source                         | Source of the numbers: can be MS or SES (via Brasil.IO) |         |                 |
| last_info_date                  | Last report date of the respective federative unit      | MS,BrIO | CC BY, CC BY-SA |

## Auxiliary files 

### Info about each municipality: `cities_info.csv`

| name               | description                                                             | sources | license |
|--------------------|-------------------------------------------------------------------------|---------|---------|
| ibge               | IBGE code of the municipality                                           | IBGE    |         |
| city               | Name of the municipality                                                | IBGE    |         |
| state              | Name of the federative unit                                             | IBGE    |         |
| region             | Name of the region                                                      | IBGE    |         |
| pop2019            | Estimated population in 2019                                            | IBGE    |         |
| pop2020            | Estimated population in 2020                                            | IBGE    |         |
| pop2021            | Estimated population in 2021                                            | IBGE    |         |
| isCountryside      | Equal to  `1` if in the countryside, or `0` if at a Metropolitan region | IBGE    |         |
| cod_RegiaoDeSaude  | ID of the "Região de Saúde"                                             |         |         |
| name_RegiaoDeSaude | Name of the "Região de Saúde"                                           |         |         |

### GPS coordinates of each municipality: `gps_cities.csv`

| name     | description                   | sources | license  |
|----------|-------------------------------|---------|----------|
| ibgeID   | IBGE code of the municipality | IBGE    |          |
| id       | Name of the municipality      | IBGE    |          |
| lat      | Latitude                      | OSM     | ODbL 1.0 |
| lon      | Longitude                     | OSM     | ODbL 1.0 |
| longName | Long name of the municipality | OSM     | ODbL 1.0 |

## Extra files

- `_control.csv`: has the last total number of deaths
- `_fixes_meta.csv`: corrections in the Ministry of Health records 
- `_tests_meta.csv`: metadata about test numbers, by date and federative unit 
- `sources.csv`: url sources of the data
- `gps_cities.csv`: cases and deaths by municipality, with GPS coordinates.
