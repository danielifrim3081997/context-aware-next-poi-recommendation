# Context-Aware Next-POI Recommendation

This project examines whether contextual information improves **next Point-of-Interest
(POI) recommendation**. Given an ordered trail of user check-ins, the models rank
candidate POIs and attempt to place the actual next POI at the top of the list.

## Cities and dataset scale

| City | Merged rows | Unique POIs | Trails |
|---|---:|---:|---:|
| Tokyo | 1,178,663 | 64,086 | 358,773 |
| Petaling Jaya | 153,543 | 18,618 | 49,718 |
| New York City | 4,849 | 1,461 | 1,177 |
| **Total** | **1,337,055** | **84,165** | **409,668** |

The reported merged-row counts describe the datasets before the modeling notebook
removes rows without a valid next-POI target.

## Models

- LightGBM Ranker
- CatBoost Ranker
- Neural TransitionRanker implemented in PyTorch

## Feature configurations

The **raw** configuration uses trajectory, temporal, geographic, transition, and
train-derived popularity features.

The **enriched** configuration additionally uses available:

- weather conditions at the prediction moment;
- holiday and opening-status context;
- candidate POI price, rating, rating-count, and tip metadata;
- candidate public-transport accessibility, stop counts, and transport modes.

## Evaluation

The notebook computes MRR, Recall@5/10/20, and NDCG@5/10/20. All models use the
same temporal trail split and sampled candidate pools. These metrics describe ranking
within the sampled pool, not full-catalogue retrieval.

## Repository structure

```text
context-aware-next-poi-recommendation/
├── README.md
├── requirements.txt
├── .gitignore
├── GITHUB_UPLOAD.md
├── notebooks/
│   ├── 01_eda_preprocessing_raw_enriched.ipynb
│   └── 02_train_evaluate_rankers.ipynb
├── data/README.md
├── results/
│   ├── README.md
│   ├── petaling_jaya_uploaded_notebook_run.csv
│   └── petaling_jaya_raw_vs_enriched.png
└── docs/
    ├── CODE_REVIEW.md
    ├── FEATURES.md
    └── VALIDATION.md
```

## Running in Google Colab

1. Upload the original V1 and V2 Parquet files to Google Drive.
2. Run `notebooks/01_eda_preprocessing_raw_enriched.ipynb` and configure
   `PROJECT_ROOT` and `DATA_DIR`.
3. The processed files are written to `PROJECT_ROOT/dataset_versions`.
4. Run `notebooks/02_train_evaluate_rankers.ipynb` once per city by changing
   `CITY_NAME` to `Tokyo`, `PetalingJaya`, or `NewYorkCity`.
5. The all-context experiment uses a separate output/cache folder named
   `next_poi_3ml_all_context_v2` so it cannot silently reuse the old feature cache.

## Running locally

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

## Data and secrets

Large Parquet files, caches, checkpoints, credentials, API keys, and tokens are
excluded from Git. Data must be obtained from their original public sources or APIs.

## Methodological note

The preprocessing notebook reproduces the uploaded unsplit preprocessing workflow.
For a stricter leakage-free experiment, split the trails first and learn imputation and
capping statistics from the training data only.
