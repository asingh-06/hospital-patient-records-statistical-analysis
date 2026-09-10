# Data Dictionary

This document describes the primary source and derived fields used in the analysis. It focuses on variables used in the analytical workflow rather than reproducing every field available in the source dataset.

## Data Relationships

```text id="odftme"
patients.Id      1 ───── * encounters.PATIENT
payers.Id        1 ───── * encounters.PAYER
encounters.Id    1 ───── * procedures.ENCOUNTER
patients.Id      1 ───── * procedures.PATIENT
```

These relationships are used to validate referential integrity and enrich encounter- and procedure-level analyses with patient and payer information.

## Encounters

| Field                 | Analytical Use                                                 |
| --------------------- | -------------------------------------------------------------- |
| `Id`                  | Unique encounter identifier                                    |
| `START`               | Encounter start timestamp; source for year, month, and quarter |
| `STOP`                | Encounter stop timestamp                                       |
| `PATIENT`             | Foreign key to `patients.Id`                                   |
| `PAYER`               | Foreign key to `payers.Id`                                     |
| `ENCOUNTERCLASS`      | Encounter/service classification                               |
| `DESCRIPTION`         | Encounter description                                          |
| `BASE_ENCOUNTER_COST` | Base encounter cost                                            |
| `TOTAL_CLAIM_COST`    | Total claim cost used in payer and cost analysis               |
| `PAYER_COVERAGE`      | Recorded payer coverage amount                                 |
| `REASONCODE`          | Encounter reason code, where available                         |
| `REASONDESCRIPTION`   | Encounter reason description, where available                  |

### Derived Encounter Fields

| Field                 | Definition                                                                                                  |
| --------------------- | ----------------------------------------------------------------------------------------------------------- |
| `year`                | Calendar year derived from `START`                                                                          |
| `month`               | Calendar month derived from `START`                                                                         |
| `quarter`             | Calendar quarter derived from `START`                                                                       |
| `year_quarter`        | Year-quarter period derived from `START`                                                                    |
| `duration_hours`      | Difference between `STOP` and `START`, expressed in hours                                                   |
| `zero_coverage`       | Boolean indicator where `PAYER_COVERAGE == 0`                                                               |
| `previous_encounter`  | Start timestamp of the immediately preceding encounter for the same patient                                 |
| `days_since_previous` | Number of days between the current and immediately preceding encounter                                      |
| `repeat_30_day`       | Indicates that the current encounter occurred 0–30 days after the patient's immediately preceding encounter |

## Patients

Patient fields used for validation, enrichment, and descriptive segmentation include:

| Field       | Analytical Use                         |
| ----------- | -------------------------------------- |
| `Id`        | Unique patient identifier and join key |
| `BIRTHDATE` | Used to derive patient age             |
| `DEATHDATE` | Patient death date, where available    |
| `GENDER`    | Descriptive patient segmentation       |
| `RACE`      | Descriptive patient segmentation       |
| `ETHNICITY` | Descriptive patient segmentation       |
| `CITY`      | Geographic attribute                   |
| `COUNTY`    | Geographic attribute                   |
| `STATE`     | Geographic attribute                   |

Demographic variables are used descriptively. The analysis does not infer causal disparities from these fields.

## Procedures

| Field               | Analytical Use                                      |
| ------------------- | --------------------------------------------------- |
| `START`             | Procedure start timestamp                           |
| `STOP`              | Procedure stop timestamp                            |
| `PATIENT`           | Foreign key to `patients.Id`                        |
| `ENCOUNTER`         | Foreign key to `encounters.Id`                      |
| `CODE`              | Procedure code                                      |
| `DESCRIPTION`       | Procedure description used for grouping and ranking |
| `BASE_COST`         | Base procedure cost                                 |
| `REASONCODE`        | Procedure reason code, where available              |
| `REASONDESCRIPTION` | Procedure reason description, where available       |

## Payers

| Field  | Analytical Use                                             |
| ------ | ---------------------------------------------------------- |
| `Id`   | Unique payer identifier and join key to `encounters.PAYER` |
| `NAME` | Readable payer name used in payer-level analysis           |

## Important Terminology

**Encounter duration** refers to elapsed time between the encounter start and stop timestamps across all encounter classes.

**Inpatient length of stay (LOS)** is used only when analysis is restricted to inpatient encounters.

**Zero recorded payer coverage** indicates that the recorded `PAYER_COVERAGE` value equals zero. It should not automatically be interpreted as uninsured status.

**30-day repeat encounter** is a project-defined utilization measure identifying an encounter occurring within 30 days of the patient's immediately preceding encounter. It is not a formal clinical readmission metric.
