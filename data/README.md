# Data Directory

Raw data are intentionally **not committed** to this repository.

## Required Files

Place these files in this directory before running the notebook:

``` text
data/
├── encounters.csv
├── patients.csv
├── procedures.csv
└── payers.csv
```

## Why the raw files are excluded

The GitHub repository is designed to demonstrate the analytical
workflow, code, documentation, and reproducibility without
redistributing the source dataset. Download the Hospital Patient Records
dataset from Maven Analytics and place the required CSV files here
locally.

## Tables Used

-   `encounters.csv` --- encounter dates, patient/payer keys, encounter
    class, encounter costs, payer coverage, and reason fields.
-   `patients.csv` --- patient demographics and geographic fields.
-   `procedures.csv` --- procedure dates, patient/encounter keys,
    descriptions, and base costs.
-   `payers.csv` --- payer identifiers and payer names.

See `../docs/DATA_DICTIONARY.md` for the analytical data model.
