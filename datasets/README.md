# Datasets

The raw datasets are not included in this repository due to file size constraints. Download them from the official sources below and place them in this folder before running the notebooks.

---

## Required Files

### 1. SEAI BER Public Search Database
- **File:** `BER.09.06.2023.zip` (or latest export)
- **Size:** ~1.5 GB (TSV)
- **Source:** [SEAI BER Public Search](https://ndber.seai.ie/BERResearchTool/Register/Register.aspx)
- **Notes:** Register for free access. Extract the TSV file. The pipeline uses `latin-1` encoding and chunked loading.

### 2. CSO Census 2022 SAPS (Small Area Population Statistics)
- **File:** `SAPS_2022_Small_Area_UR_171024.csv`
- **Source:** [CSO Census 2022 Small Area Statistics](https://www.cso.ie/en/census/census2022/census2022smallareapopulationstatistics/)
- **Notes:** Download the Small Area-level SAPS table. Contains all socioeconomic indicators used for feature engineering.

### 3. Tailte Éireann Small Area Boundaries
- **File:** `SMALL_AREA_2022_Genralised_20m_view.geojson`
- **Source:** [Tailte Éireann Open Data](https://data.gov.ie/dataset/small-areas-osi-national-statistical-boundaries-2022)
- **Notes:** Use the 2022 generalised 20m boundary file for correct SA_Code alignment with Census 2022.

---

Once downloaded, place all three files in this `datasets/` folder and run the notebooks in order:
1. `notebooks/Energy Poverty Pipeline 1.ipynb` — EDA
2. `notebooks/Energy Poverty Pipeline 2.ipynb` — Full pipeline
