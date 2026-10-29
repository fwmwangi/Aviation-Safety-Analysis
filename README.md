# Aviation Accidents Analysis

Aviation safety analysis for a consulting engagement: which aircraft makes/models show low
rates of total destruction and low likelihood of fatal or serious injuries in an accident.

## Status

This package is **partial**. It contains the data layer and the completed, executed cleaning
notebook. The analysis notebook, the README visual/report sections and the exported figures
were not finished before the session ended.

| Component | Status |
| --- | --- |
| Raw data + state lookup | Complete (verbatim copies of the supplied files) |
| `01_Aviation_Accidents_Cleaning.ipynb` | Complete, executed end-to-end, 0 errors |
| Cleaned dataset `data/aviation_cleaned.csv` | Complete, 18,072 rows x 37 columns |
| Analysis notebook (EDA, make/model injury and destruction rates) | **Missing** |
| Exported figures (`images/`) | **Empty** — the folder exists but no figures were saved |

## Contents

```
.
├── README.md
├── data/
│   ├── aviation_raw.csv        # NTSB-style accident data, 88,889 rows x 31 columns
│   ├── lookup_states.csv       # US state name / abbreviation lookup, 63 lines
│   └── aviation_cleaned.csv    # output of the cleaning notebook, 18,072 x 37
├── notebooks/
│   └── 01_Aviation_Accidents_Cleaning.ipynb
└── images/                     # reserved for exported figures (currently empty)
```

## Pipeline

`notebooks/01_Aviation_Accidents_Cleaning.ipynb` reads `data/aviation_raw.csv` (cp1252
encoding), applies the cleaning and filtering rules, writes `data/aviation_cleaned.csv`,
then reloads the file to verify it. The notebook resolves its paths relative to the project
root, so it runs whether the working directory is the repo root or `notebooks/`.

Recorded results from the executed notebook:

- raw input: 88,889 rows x 31 columns
- final cleaned frame: 18,072 rows x 37 columns
- reload check: 18,072 rows x 37 columns

## Reproducing

```bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter nbconvert --to notebook --execute --inplace notebooks/01_Aviation_Accidents_Cleaning.ipynb
```

## Not included

No GitHub repository was created or pushed for this work. The analysis notebook and its
figures still need to be written against `data/aviation_cleaned.csv`.

