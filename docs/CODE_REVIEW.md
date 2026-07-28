# Code review notes

## Changes made

- Cleared notebook outputs, execution counters, and Colab-only metadata.
- Centralized project, dataset, and output paths.
- Added automatic file resolution for all three cities.
- Added README, requirements, ignore rules, data instructions, and upload instructions.
- Changed LightGBM categorical vocabularies to be learned from training data only.
- Added weather, holiday/opening, POI metadata, and public-transport columns to the
  enriched candidate feature matrix.
- Added runtime assertions confirming that temperature and public-transport fields
  reach the models.
- Changed the all-context output directory to prevent reuse of the old feature cache.
- Scanned for obvious API keys, passwords, tokens, and secrets; none were found.

## Important methodological limitations

### Unsplit preprocessing

Imputation and capping values in the preprocessing notebook are estimated on the full
city dataset. A strict final experiment should fit them on training data only.

### Sampled-candidate evaluation

Each query is evaluated against the true next POI and a limited number of hard
negatives. Results are not full-catalogue recommendation metrics.

### Recall@20

With ten negatives per positive, most groups contain at most eleven candidates, making
Recall@20 weakly informative and often identical across models.

### Existing result artifacts

The committed Petaling Jaya CSV and plot were extracted from the uploaded notebook
before the all-context feature fix. They are preserved only as historical artifacts.
The three models must be rerun for all cities before reporting final all-context results.

### Cross-validation

The workflow uses one chronological 80/20 trail split. Future work should consider
multiple seeds or repeated temporal splits to estimate variance.
