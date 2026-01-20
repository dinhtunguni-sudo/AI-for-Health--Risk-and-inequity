# Fairness and Calibration Analysis

## Objective
Beyond overall predictive accuracy, models used in public health must be evaluated for
consistency, reliability, and equity across settings. This step assesses whether risk
prediction models for low UHC service coverage perform comparably across population strata
and whether predicted risks are appropriately calibrated.

The goal is to reduce the risk that data-driven tools may unintentionally reinforce existing
health inequities when applied in real-world decision-making.

---

## Why fairness and calibration matter in public health
In population health applications, models are often used to prioritise settings for additional
support or intervention. If predictive performance varies systematically across income groups
or regions, such tools may disadvantage settings that already face structural barriers.

Calibration is particularly important because poorly calibrated risk scores can lead to
over- or under-estimation of need, even when discrimination metrics appear acceptable.

---

## Subgroup definitions
Model performance is evaluated across the following population strata:

- **Income group:** World Bank income classification (e.g. low, lower-middle, upper-middle, high)
- **Geographic region:** World Health Organization (WHO) regions

These groupings reflect commonly used policy and reporting categories in global health.

---

## Subgroup performance evaluation
For each subgroup, we examine:

- AUROC (discrimination)
- AUPRC (performance under class imbalance)
- Recall for low-coverage settings
- Sample size and outcome prevalence

Performance metrics are interpreted with caution in subgroups with limited sample sizes.

Differences in performance are not assumed to reflect algorithmic bias alone and may arise
from structural data limitations, reporting quality, or unmeasured contextual factors.

---

## Calibration analysis
Calibration assesses whether predicted risks correspond to observed outcome frequencies.

We evaluate:
- Overall calibration using reliability curves
- Subgroup-specific calibration, with particular attention to lower-income settings

Poor calibration in disadvantaged groups is of particular concern, as it may lead to systematic
underestimation of risk in settings where early identification is most needed.

---

## Error analysis with an equity lens
False negatives—settings with low service coverage that are not flagged as high risk—are examined
by income group and region.

From a public health perspective, these errors are especially consequential, as they represent
missed opportunities for early support. Common characteristics of such cases (e.g. higher
missingness, inconsistent reporting) are summarised where possible.

---

## Interpretation and safeguards
Observed differences in subgroup performance highlight the need for safeguards when using
predictive models in public health contexts. These include:

- Routine monitoring of subgroup performance
- Conservative thresholds when prioritising underserved settings
- Use of risk scores to trigger additional review or support, rather than automated decisions

Models should augment, not replace, expert judgment and contextual knowledge.

---

## Limitations
This analysis relies on aggregated, country-level data and cannot capture within-country
heterogeneity. Subgroup analyses are limited by data availability and reporting quality in
some settings.

Fairness assessment in this context is therefore exploratory and should be revisited as
more granular and higher-quality data become available.

---

## Implications for responsible use
When evaluated transparently and applied with appropriate safeguards, risk prediction models
can support public health planning without exacerbating inequities. Explicit attention to
fairness and calibration is essential to ensure that data-driven tools align with the core
principles of equity and social justice in public health.

---

## Summary
This step demonstrates the importance of moving beyond overall accuracy to assess how predictive
models behave across populations and contexts. Incorporating fairness and calibration analyses
is critical for the responsible application of machine learning in population health.
