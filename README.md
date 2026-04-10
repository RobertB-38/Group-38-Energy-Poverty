# Group 38 — Energy Poverty Risk Classification in Ireland

**Module:** CSC1144 Data Analytics & Data Mining — DCU MSc Computing (Data Analytics), 2025–26  
**Group members:** Robert Borkar, Niket Ahire, Selwyn Gonsalves, Rachel Kunjumon  
**Supervisor:** Prof. Andrew McCarren

---

## Project Overview

This project builds a machine learning pipeline to classify **energy poverty risk** across Ireland's ~18,916 Small Areas (Census 2022). The final model is a **Random Forest binary classifier** (High Risk / Not At Risk) achieving:

- **Test Accuracy:** 84.96%
- **CV Accuracy:** 84.82% ± 0.22%
- **F1-Score:** 0.85 (symmetric across both classes)

Outputs are intended to support SEAI's National Retrofitting Scheme for geographic targeting.

---

## Repository Structure

```
├── notebooks/
│   ├── Energy Poverty Pipeline 1.ipynb   # EDA: BER distribution, urban/rural split, coverage
│   └── Energy Poverty Pipeline 2.ipynb   # Full ML pipeline: feature engineering, modelling, evaluation
│
├── outputs/
│   ├── eda_01_ber_distribution.png        # BER rating distribution across Small Areas
│   ├── eda_02_urban_rural.png             # Urban vs rural breakdown
│   ├── eda_03_ber_coverage.png            # BER coverage by Small Area
│   ├── feature_importance_final_rf.png    # Random Forest feature importances
│   ├── confusion_matrix_final.png         # Final model confusion matrix
│   ├── map_energy_poverty_risk.png        # Choropleth: predicted High Risk Small Areas
│   └── energy_poverty_spatial_dataset.geojson  # Merged spatial dataset (all features + predictions)
│
├── datasets/
│   └── README.md                          # Dataset sources and download instructions
│
└── report/
    └── (IEEE paper — to be added)
```

---

## Pipeline Summary

| Stage | Detail |
|---|---|
| Data sources | CSO Census 2022 SAPS, SEAI BER Public Search (1.49GB TSV), Tailte Éireann SA boundaries |
| BER loading | Chunked ingestion, latin-1 encoding, bad-line handling |
| Feature engineering | Socioeconomic rates from SAPS (welfare, medical card, social housing, old-age payment, family with children) |
| Missing data | MissForest imputation for ~2,153 missing BER Small Areas |
| Urban bias correction | `no_car_rate` capped at 20%, `old_housing_rate` capped at 45% for urban SAs |
| Spatial lag | Queen contiguity (Moran's I = 0.3031, p=0.001) via libpysal + esda |
| Target variable | Binary: BER D-or-below AND compound socioeconomic condition |
| Class imbalance | `class_weight='balanced'` (SMOTE rejected — synthetic SAs are policy-meaningless) |
| Hyperparameter tuning | Optuna (100 trials, TPE sampler); `max_depth` 19→10 to reduce overfitting gap to 5.06% |
| Final model | Random Forest, 84.96% test accuracy |

---

## Requirements

```
python >= 3.10
pandas, numpy, geopandas, libpysal, esda
scikit-learn, xgboost, optuna
matplotlib, seaborn, folium
```

---

## Data Sources

See `datasets/README.md` for download links and instructions.
