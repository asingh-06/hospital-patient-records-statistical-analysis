# Limitations

The following limitations should be considered when interpreting the results of this analysis.

## 1. Synthetic Data

The dataset contains synthetic healthcare records. It is appropriate for analytical and educational purposes but should not be used for clinical decision-making or evaluation of real healthcare organizations, patients, or payers.

## 2. Incomplete 2022 Data

The encounter data end in early February 2022. Therefore, 2022 represents only a partial year and should not be interpreted as a complete calendar year or directly compared with prior full-year encounter volumes.

## 3. Project-Defined Repeat-Utilization Metric

The 30-day repeat encounter measure identifies encounters occurring within 30 days of the immediately preceding encounter for the same patient.

This metric is intended to measure repeat healthcare utilization and should not be interpreted as a formal hospital readmission rate.

## 4. Extreme Encounter-Duration Values

Extreme encounter-duration records were retained and described rather than automatically removed.

These observations may represent unusual synthetic records, data-generation artifacts, or other conditions requiring additional validation. Their presence can substantially influence mean-based duration statistics.

## 5. Payer-Coverage Ambiguity

`PAYER_COVERAGE == 0` represents an observed value in the dataset and does not by itself establish that a patient was uninsured.

Zero recorded coverage may have multiple explanations, so the analysis refers to these records as **zero recorded payer coverage** rather than uninsured encounters.

## 6. Statistical Association Does Not Establish Causation

The chi-square and Spearman correlation analyses identify statistical relationships between variables.

These results do not establish causal mechanisms, and statistically significant relationships should not be interpreted as evidence that one variable causes another.

## 7. No Case-Mix Adjustment

Payer-level cost comparisons are descriptive and are not adjusted for patient severity, encounter class, procedure mix, demographic characteristics, or other clinical and utilization factors.

As a result, differences in average or median claim cost should not be interpreted as direct measures of payer performance.

## 8. Different Cost Measures

Procedure `BASE_COST` and encounter `TOTAL_CLAIM_COST` represent different cost constructs and should not be treated as interchangeable measures.

Procedure-level cost analysis and encounter-level claim-cost analysis are therefore interpreted separately.

## 9. Descriptive Demographic Analysis

Patient demographic variables are used for descriptive segmentation only.

Observed differences across demographic groups do not by themselves establish healthcare disparities, inequities, or causal group differences.

## 10. Available Fields Constrain Interpretation

The analysis is limited to variables available in the source dataset.

Some operational and clinical questions would require additional information, such as standardized admission and discharge definitions, diagnosis detail, severity indicators, clinical outcomes, staffing information, or workflow metadata.

These limitations define the appropriate boundaries for interpreting the analytical findings and recommendations.
