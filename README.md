# Hospital Patient Records — Statistical & Healthcare Operations Analysis

A healthcare analytics project using **Python, pandas, SciPy, Matplotlib, and Jupyter** to evaluate patient utilization, encounter patterns, payer coverage, procedure activity, healthcare costs, and data quality using synthetic hospital records.

## Executive Summary

This project analyzes synthetic hospital patient records spanning **January 2011 through February 2022**. The dataset includes:

* **27,891 encounters**
* **974 patients**
* **47,701 procedure records**
* **10 payer records**

The analysis combines exploratory data analysis, statistical testing, healthcare operations analysis, and patient-utilization analysis to identify patterns that may support operational and financial decision-making.

### Key Results

* Encounter volume increased from **1,336 encounters in 2011** to **3,530 in 2021**, an increase of approximately **164.2%**.
* **Ambulatory care** was the largest encounter class, accounting for **12,537 encounters**.
* **13,586 encounters (48.7%)** had zero recorded payer coverage.
* Encounter class and zero recorded payer coverage were statistically associated (**χ² = 381.13, Cramér's V = 0.117**).
* Encounter duration was highly right-skewed, with a **median of 0.25 hours** and **P95 of 3.80 hours**.
* The project-defined 30-day repeat-utilization metric identified **17,262 repeat encounters across 772 unique patients**.
* The most frequent procedure was **Assessment of health and social care needs**, with **4,596 records**.
* **Medicaid** had the highest descriptive average claim cost at approximately **$6,205 per encounter**.
* Encounter duration and total claim cost demonstrated a **moderate positive monotonic association (Spearman ρ = 0.338)**.

Statistical relationships are interpreted as associations and not as evidence of causation.

---

## Business Questions

The analysis addresses the following questions:

1. How has encounter volume changed over time?
2. What is the encounter-class mix, and how has it changed?
3. How long do encounters last, and how should a highly skewed duration distribution be summarized?
4. How common is zero recorded payer coverage, and does it vary by encounter class?
5. Which procedures are most frequent, most costly, and most operationally significant when volume and cost are considered together?
6. How do average and median claim costs vary by payer?
7. How many unique inpatient patients are seen each quarter?
8. Which patients demonstrate the greatest repeat utilization?
9. Is encounter duration associated with total claim cost?

---

## Repository Structure

```text
hospital-patient-records-statistical-analysis/
│
├── README.md
├── .gitignore
├── requirements.txt
│
├── data/
│   └── README.md
│
├── notebooks/
│   └── hospital_patient_records_complete_analysis.ipynb
│
├── docs/
│   ├── DATA_DICTIONARY.md
│   ├── METHODOLOGY.md
│   ├── FINDINGS.md
│   ├── RECOMMENDATIONS.md
│   └── LIMITATIONS.md
│
├── results/
│   ├── README.md
│   └── generated analytical outputs
│
└── figures/
    └── generated visualizations
```

---

## Analytical Workflow

The analysis follows a structured workflow:

**Business Problem → Data Source → Data Understanding → Data Quality Assessment → Data Cleaning & Transformation → Exploratory Data Analysis → Statistical Analysis → Healthcare Operations Analysis → Cost & Payer Analysis → Patient Utilization Analysis → Findings → Recommendations → Limitations → Next Phase Analysis → Conclusion**

Separating data-quality assessment, transformations, statistical evidence, and business interpretation helps keep analytical assumptions and decisions transparent.

---

## Statistical Methods

| Method                 | Purpose                                                                           |
| ---------------------- | --------------------------------------------------------------------------------- |
| Descriptive statistics | Summarize encounter volume, costs, payer coverage, procedures, and utilization    |
| Median and percentiles | Describe highly skewed encounter-duration distributions                           |
| Chi-square test        | Test the association between encounter class and zero recorded payer coverage     |
| Cramér's V             | Measure the strength of the chi-square association                                |
| Spearman correlation   | Measure the monotonic association between encounter duration and total claim cost |
| Grouped aggregation    | Analyze utilization, procedures, inpatient activity, and payer measures           |

---

## Data Quality Assessment

Before performing the primary analysis, the datasets were evaluated for:

* Duplicate records and identifiers
* Missing values
* Invalid encounter dates
* Negative cost values
* Invalid payer-coverage values
* Referential-integrity issues
* Encounter-duration anomalies

Extreme duration records were retained rather than automatically removed.

An important distinction was identified in the duration data: **1,077 encounters were exactly 24 hours**, while only **75 encounters exceeded 24 hours**. These observations were therefore evaluated separately rather than treating all encounters of 24 hours or longer as equivalent anomalies.

---

## Key Analytical Definitions

### Zero Recorded Payer Coverage

An encounter is classified as having zero recorded payer coverage when:

`PAYER_COVERAGE == 0`

This describes the value recorded in the dataset and should **not automatically be interpreted as uninsured status**.

### Encounter Duration

Encounter duration is calculated as the difference between the encounter stop and start timestamps.

The term **encounter duration** is used across all encounter classes. **Length of stay** is reserved for analyses restricted to inpatient encounters.

### 30-Day Repeat Encounter

A repeat encounter is defined as an encounter occurring within **30 days of the immediately preceding encounter for the same patient**.

This measure is used to analyze repeat healthcare utilization and should **not be interpreted as a formal clinical readmission rate**.

---

## Healthcare Operations Analysis

Operational analysis includes:

* Annual encounter trends
* Encounter-class distribution and trends
* Quarterly inpatient utilization
* Encounter-duration distributions
* Procedure frequency
* Procedure cost
* Procedure volume-versus-cost analysis
* Repeat patient utilization

Procedure cost rankings use a minimum observation threshold to reduce the influence of procedures represented by very small numbers of records.

---

## Cost & Payer Analysis

Payer analysis evaluates:

* Encounter volume
* Average claim cost
* Median claim cost
* Payer coverage
* Zero recorded payer coverage

Payer comparisons are **descriptive rather than performance rankings**.

Differences in claim costs may reflect encounter class, patient characteristics, procedure mix, severity, and other case-mix factors that are not controlled for in this analysis.

---

## Recommendations

Based on the analytical findings, the project recommends:

1. Investigating the causes of zero recorded payer coverage.
2. Monitoring utilization separately by encounter class.
3. Using median, P90, and P95 duration metrics alongside the mean.
4. Monitoring patients with frequent 30-day repeat encounters.
5. Evaluating procedures using both utilization volume and financial impact.
6. Applying case-mix adjustment before interpreting payer cost differences as performance differences.

See [`docs/RECOMMENDATIONS.md`](docs/RECOMMENDATIONS.md) for additional detail.

---

## Reproducing the Analysis

### 1. Obtain the Data

Download the **Hospital Patient Records** dataset from Maven Analytics.

### 2. Add the Source Files

Place the following files in the local `data/` directory:

```text
data/
├── encounters.csv
├── patients.csv
├── procedures.csv
└── payers.csv
```

Raw source files are intentionally excluded from version control.

### 3. Create a Python Environment

Create and activate a Python virtual environment.

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Run the Analysis

Open:

```text
notebooks/hospital_patient_records_complete_analysis.ipynb
```

Run the notebook from top to bottom to reproduce the analysis.

---

## Tools & Technologies

* Python
* pandas
* NumPy
* SciPy
* Matplotlib
* Jupyter Notebook
* Git
* GitHub

---

## Data Source

This project uses the **Maven Analytics Hospital Patient Records** synthetic dataset, which is based on Synthea-generated electronic health record data.

Because the records are synthetic, the project is intended for analytical and educational purposes rather than clinical decision-making.

---

## Project Documentation

Additional documentation is available in the `docs/` directory:

* [`DATA_DICTIONARY.md`](docs/DATA_DICTIONARY.md) — datasets, relationships, fields, and derived variables
* [`METHODOLOGY.md`](docs/METHODOLOGY.md) — analytical definitions and statistical methodology
* [`FINDINGS.md`](docs/FINDINGS.md) — major findings, supporting evidence, and business implications
* [`RECOMMENDATIONS.md`](docs/RECOMMENDATIONS.md) — recommended actions based on the analysis
* [`LIMITATIONS.md`](docs/LIMITATIONS.md) — analytical and interpretation limitations

---

## Disclaimer

This project analyzes **synthetic healthcare data**. Results should not be used for patient care, clinical decisions, insurance decisions, or evaluation of real healthcare organizations or payers.
