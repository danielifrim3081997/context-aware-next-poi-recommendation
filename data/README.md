# Data files

Data are not included in this repository because the Parquet files are large and may
be subject to the terms of their original datasets and APIs.

## Expected original enriched files

- `Tokyo_V2_context_enriched_LOCAL.parquet`
- `PetalingJaya_V2_context_enriched_LOCAL.parquet`
- `NewYorkCity_V2_context_enriched_LOCAL.parquet`

## Expected original raw files

- `Tokyo_V1_baseline_no_context.parquet`
- `PetalingJaya_V1_baseline_no_context.parquet`
- `NewYorkCity_V1_baseline_no_context.parquet`

## Generated model inputs

The preprocessing notebook writes:

- `<City>_V1_preprocessed_unsplit_all_rows.parquet`
- `<City>_V2_preprocessed_unsplit_all_rows.parquet`

to `PROJECT_ROOT/dataset_versions`.
