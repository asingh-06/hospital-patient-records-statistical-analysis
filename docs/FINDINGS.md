# Findings

Each finding is presented using the structure **Finding → Evidence → Business Implication**.

## 1. Encounter Volume Increased Materially

**Finding:** Encounter volume increased substantially between 2011 and 2021.

**Evidence:** Annual encounters increased from **1,336 in 2011** to **3,530 in 2021**, an increase of approximately **164.2%**.

**Business Implication:** Capacity and staffing analysis should identify which encounter classes and service lines are contributing to increased utilization rather than relying only on total encounter volume.

> **Note:** The dataset contains only a partial year for 2022, so 2022 should not be interpreted as a full-year decline.

## 2. Ambulatory Care Dominates the Encounter Mix

**Finding:** `ambulatory` is the largest encounter class.

**Evidence:** Ambulatory encounters account for **12,537 records**, approximately **45.0%** of all encounters.

**Business Implication:** Operational planning should account for the dominant ambulatory workload while maintaining separate views of inpatient, emergency, outpatient, urgent-care, and wellness activity.

## 3. Encounter Duration Is Highly Right-Skewed

**Finding:** Typical encounter duration is substantially lower than values in the extreme upper tail of the distribution.

**Evidence:** Median encounter duration is **0.25 hours**, while P95 is **3.80 hours** and the maximum is approximately **44,930 hours**. There are **1,077 encounters exactly 24 hours long** and only **75 encounters longer than 24 hours**.

**Business Implication:** Median and percentile measures such as P90 and P95 provide more representative operational indicators than the mean alone. Extreme-duration records should be monitored separately and reviewed for potential data-quality or operational explanations.

## 4. Zero Recorded Payer Coverage Is Common

**Finding:** A substantial proportion of encounters have zero recorded payer coverage, and the prevalence differs by encounter class.

**Evidence:** **13,586 encounters (48.7%)** have `PAYER_COVERAGE == 0`. Encounter class and zero recorded payer coverage are statistically associated (**χ² = 381.13, p < 0.001; Cramér's V = 0.117**). The effect size indicates that the association is relatively weak despite being statistically significant.

**Business Implication:** Coverage completeness and payer workflows warrant further review. Because zero recorded coverage may have multiple explanations, it should not automatically be interpreted as uninsured status.

## 5. Repeat Utilization Is Widespread Under the Project Definition

**Finding:** Many patients have encounters occurring within 30 days of a preceding encounter.

**Evidence:** The project-defined measure identifies **17,262 repeat encounters across 772 unique patients**.

**Business Implication:** Patients with frequent repeat encounters can be monitored as a distinct utilization group to support care-coordination review, follow-up analysis, and resource planning.

The 30-day repeat measure is a utilization indicator and should **not** be reported as a formal clinical readmission rate.

## 6. Procedure Frequency and Cost Identify Different Priorities

**Finding:** High-frequency procedures are not necessarily the same procedures that have the highest average cost.

**Evidence:** **Assessment of health and social care needs** is the most frequent procedure with **4,596 records**. Procedure analysis separately evaluates frequency, average base cost, median base cost, and total financial impact.

**Business Implication:** Procedure prioritization should consider both utilization volume and financial impact. High-volume procedures may present workflow-improvement opportunities, while high-cost procedures may warrant focused financial and resource review.

## 7. Payer Claim Costs Vary Materially

**Finding:** Descriptive claim costs differ across payers.

**Evidence:** **Medicaid** has the highest descriptive average total claim cost in the dataset at approximately **$6,205 per encounter**.

**Business Implication:** Payer-level cost variation can identify areas for deeper analysis, but it should not be interpreted as evidence of payer performance without adjusting for encounter class, patient characteristics, procedure mix, severity, and other case-mix factors.

## 8. Encounter Duration and Claim Cost Have a Moderate Positive Association

**Finding:** Encounter duration has a moderate positive monotonic association with total claim cost.

**Evidence:** Spearman correlation analysis produced **ρ = 0.338 (p < 0.001)**.

**Business Implication:** Encounter duration may be a useful explanatory variable in future cost analysis or modeling. However, the observed relationship is associative and should not be interpreted as evidence that longer encounter duration causes higher claim costs.
