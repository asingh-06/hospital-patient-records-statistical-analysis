# Methodology

This document describes the analytical methods, definitions, and assumptions used in the analysis.

## 1. Data Understanding

The analysis begins by inspecting dataset dimensions, column names, data types, missing values, and unique values across the encounters, patients, procedures, and payers datasets.

Relationships between the datasets are also reviewed to confirm the keys required for patient-, encounter-, procedure-, and payer-level analysis.

## 2. Data Quality Assessment

Data-quality checks include:

* Duplicate records and identifiers
* Missing values
* Invalid encounter start and stop sequences
* Negative cost values
* Payer-coverage validity
* Referential integrity between related datasets
* Encounter-duration anomalies

Extreme duration values are not automatically removed. Retaining these observations preserves the source data and avoids arbitrary filtering before their characteristics are understood.

The analysis also distinguishes encounters lasting **exactly 24 hours** from those **exceeding 24 hours**.

## 3. Data Cleaning and Transformation

Date fields are converted to datetime values.

Calendar year, month, quarter, and year-quarter are derived from the encounter `START` timestamp. Encounter duration is calculated as the difference between `STOP` and `START`, expressed in hours.

A zero-coverage indicator is created using:

`PAYER_COVERAGE == 0`

For repeat-utilization analysis, encounters are sorted by patient and encounter start time. The immediately preceding encounter is identified using `groupby().shift(1)`, and the interval between encounters is calculated in days.

Patient and payer information is joined to encounter-level data using the documented relational keys.

## 4. Repeat Encounter Definition

A **30-day repeat encounter** is defined as an encounter occurring between 0 and 30 days after the immediately preceding encounter for the same patient.

Using this definition, the analysis identifies **17,262 repeat encounters across 772 unique patients**.

This measure is intentionally not labeled a clinical readmission rate because it does not apply formal admission and discharge eligibility rules, index-admission logic, transfer exclusions, planned-readmission exclusions, or condition-specific definitions.

It should therefore be interpreted as a measure of **repeat healthcare utilization**.

## 5. Encounter-Duration Analysis

Encounter duration is highly right-skewed, so the analysis emphasizes robust summary measures such as the median and percentiles rather than relying on the mean alone.

The observed median encounter duration is **0.25 hours**, and P95 is **3.80 hours**.

Visualizations may restrict the displayed range to improve readability; however, the underlying extreme observations remain in the analytical dataset unless explicitly stated otherwise.

The term **encounter duration** is used for analysis across all encounter classes. **Length of stay (LOS)** is reserved for inpatient-specific analysis.

## 6. Chi-Square Test and Cramér's V

A chi-square test of independence is used to evaluate whether encounter class and zero recorded payer coverage are statistically associated.

Cramér's V is reported alongside the chi-square result to quantify the strength of the association.

The analysis produced:

* **χ² = 381.13**
* **p < 0.001**
* **Cramér's V = 0.117**

The results indicate a statistically significant but relatively weak association between encounter class and zero recorded payer coverage.

Statistical association does not establish causation.

## 7. Spearman Rank Correlation

Spearman rank correlation is used to evaluate the monotonic relationship between encounter duration and total claim cost.

Spearman correlation is appropriate for this analysis because the variables are skewed and contain extreme observations, and the method does not require a linear relationship or normally distributed variables.

The analysis produced:

* **Spearman ρ = 0.338**
* **p < 0.001**

This indicates a moderate positive monotonic association between encounter duration and total claim cost.

The result is associative and does not establish that longer encounter duration causes higher claim costs.

## 8. Procedure Analysis

Procedures are evaluated using:

* Procedure frequency
* Average base cost
* Median base cost
* Total base cost

Average-cost rankings use a minimum procedure-count threshold to reduce the influence of procedures represented by very small numbers of observations.

A volume-versus-cost analysis is also used to distinguish procedures based on both utilization and financial impact rather than relying on a single measure.

## 9. Payer Analysis

Payer-level analysis evaluates:

* Encounter volume
* Average total claim cost
* Median total claim cost
* Recorded payer coverage
* Zero recorded payer coverage

These comparisons are descriptive.

Payers are not ranked as better or worse because the analysis does not adjust for encounter class, patient characteristics, severity, procedure mix, or other case-mix factors that may influence claim costs.

## 10. Patient Utilization Analysis

Patient utilization is summarized using encounter counts, repeat encounters, total claim costs, and encounter history.

High utilization is identified using a percentile-based threshold rather than an arbitrary fixed encounter count. In this analysis, the **90th percentile of patient encounter counts** is used as the threshold for identifying high-utilization patients.

The resulting group is intended to support additional utilization analysis and should not be interpreted as a clinical risk classification.

All patient identifiers and records in the dataset are synthetic.
