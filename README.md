# Pipeline de Dados — Portal da Transparência 🇧🇷

Pipeline de engenharia de dados end-to-end extraindo dados reais do 
Portal da Transparência do Governo Federal Brasileiro.

## Stack
- **Extração**: Python 3.13 + requests
- **Data Lake**: Google Cloud Storage (Bronze / Silver)
- **Data Warehouse**: BigQuery (Gold)
- **Transformação**: dbt Core
- **Qualidade**: Great Expectations
- **Orquestração**: Apache Airflow
- **Linhagem**: OpenLineage
- **CI/CD**: GitHub Actions

## Arquitetura
```
Portal da Transparência API
        ↓
   GCS Bronze  →  dados brutos, particionados por data
        ↓
   Great Expectations  →  validação de qualidade
        ↓
   GCS Silver  →  limpo, tipado, deduplicado
        ↓
   dbt Core  →  modelagem dimensional (dim_* / fct_*)
        ↓
   BigQuery Gold  →  pronto para consumo analítico
        ↓
   Airflow  →  orquestra todo o fluxo
```

## Estrutura
```
├── dags/           # DAGs do Airflow
├── dbt/            # Projeto dbt (staging → intermediate → marts)
├── src/
│   ├── extractors/ # Scripts de extração por endpoint
│   ├── loaders/    # Carregamento GCS e BigQuery
│   └── utils/      # HTTP client, retry, logging
├── expectations/   # Suites Great Expectations
├── tests/          # Testes unitários (pytest)
├── infra/          # Scripts de infraestrutura GCP
└── .github/        # Pipelines CI/CD
```

## Status
🚧 Em construção — Fase 1: Fundação