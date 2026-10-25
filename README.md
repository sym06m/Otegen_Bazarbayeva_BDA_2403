# Location-level pedestrian crash risk with spatial cross-validation

Course project, Research Methods and Tools, Astana IT University.
Authors: Otegen Symbat, Bazarbayeva Balslu

## What this repository contains

| Path | Content |
|---|---|
| `notebooks/notebook1_intersection_dataset.ipynb` | Downloads NYC crash records, builds the location-level dataset (executed, outputs included) |
| `notebooks/notebook2_models_spatial_cv.ipynb` | Models, spatial block cross-validation, bootstrap CIs, tests, error analysis, figures (executed, outputs included) |
| `data/intersections.csv` | The exact location-level dataset used in the paper (36,679 locations) |
| `results/` | Figures (PDF) and result tables (CSV) reported in the paper |
| `requirements.txt` | Package versions used |

## Data

Source: NYC Open Data, "Motor Vehicle Collisions - Crashes" (NYPD),
https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95 (accessed October 2026).
The portal data can be revised over time, so `data/intersections.csv` is the exact file behind the reported numbers.

- Unit of analysis: map cell of 0.001 degrees (about 100 m), because street-name pairs and coordinates are almost never present in the same record.
- Features are built from crashes in 2021-2022; the target (pedestrian injured or killed in 2023-2024) comes from the later period.
- Spatial blocks: cells of 0.02 degrees (about 2 km), assigned to 5 folds at random per seed.
- No direct pedestrian or traffic exposure data is used (see the paper for this limitation).

## How to reproduce

1. Run `notebook1_intersection_dataset.ipynb` (about 5 minutes). It saves `intersections.csv`.
2. Run `notebook2_models_spatial_cv.ipynb` (about 27 minutes on 2 CPU cores). Upload `intersections.csv` when asked. To skip step 1, use `data/intersections.csv`.

Both notebooks were run in Google Colab (CPU only, no GPU).

## Environment and settings

Python 3.13, numpy 2.1.3, pandas 2.2.3, scikit-learn 1.6.1, xgboost 3.4.1, imbalanced-learn 0.14.2.
Seeds 0-4, 5 spatial folds, 500 bootstrap resamples, total running time of notebook 2: 26.9 minutes.
