# AI-for-Health--Risk-and-inequity
Applied machine learning for population health and health service coverage using open data

Access to essential health services remains uneven across countries and over time. Despite global efforts toward Universal Health Coverage (UHC), many settings continue to experience persistently low service coverage, often driven by structural and socioeconomic constraints.

This project explores how applied machine learning, using open, population-level data, can support public health analysis by identifying country-year settings at higher risk of low health service coverage. The focus is not on algorithmic novelty, but on responsible, interpretable, and equity-aware use of ML to complement traditional public health surveillance and planning.

**Research Objectives**

This project addresses three main questions:
1.Risk prediction
Can routinely available population-level indicators be used to predict settings with low coverage of essential health services?
2. Equity and subgroup performance
Does model performance differ across socioeconomic or regional groups, and what are the implications for equity-sensitive use of ML in public health?
3. Public health relevance
How might such predictive signals be used to support prioritisation and planning, while avoiding unintended reinforcement of existing inequities?

**Outcome Definition**
The primary outcome is the Universal Health Coverage (UHC) Service Coverage Index (SDG 3.8.1), a composite indicator developed by the WHO and World Bank to track coverage of essential health services.

For modeling purposes, the task is framed as a binary classification problem:
- Low coverage is defined as country-year observations falling within the lowest quartile of the UHC Service Coverage Index for a given year.
- All other observations are classified as not low coverage.
This formulation reflects a policy-relevant perspective focused on identifying potentially underserved settings.

**Data Sources**
The analysis relies exclusively on publicly available, aggregated data, including:
- Our World in Data (OWID): UHC Service Coverage Index and selected health, demographic, and socioeconomic indicators.
- Optional supplementary indicators from World Bank and WHO datasets where appropriate.
No individual-level or sensitive data are used.

**Methods
Modeling approach**
The analysis uses classical machine learning models commonly applied in population-level health research:
- Logistic Regression (baseline, interpretable)
- Random Forest (non-linear comparison)
**Evaluation strategy**
- Temporal train–test split to reflect real-world forecasting scenarios
- Primary metrics: AUROC and AUPRC
- Additional focus on recall for low-coverage settings, reflecting public health priorities
**Equity and calibration analysis**
Model performance and calibration are evaluated across:
- World Bank income groups
- Geographic regions
This step is central to assessing whether predictive performance is consistent across population strata.

**Key Findings**
Overall predictive performance
Using population-level open data, the best-performing model achieved an AUROC of [X.XX] and an AUPRC of [X.XX] on temporally held-out test data. These results indicate meaningful discrimination for identifying settings with low UHC service coverage, beyond prevalence-based baselines.

**Feature patterns**
Indicators related to health system capacity and socioeconomic conditions consistently contributed to model predictions. These patterns align with established public health evidence and suggest that the model captures structural determinants rather than spurious associations.

**Equity and subgroup performance**
Predictive performance varied across income groups and regions. In particular, performance and calibration were generally weaker in lower-income settings, highlighting the need for caution when applying predictive models in contexts with greater data limitations.

**Public health relevance**
From a public health perspective, false negatives—settings incorrectly classified as not at risk—are of particular concern. Many such cases were associated with higher missingness or noisier reporting, suggesting that limitations arise from data quality rather than algorithmic bias alone.

Public Health Implications
When used with appropriate safeguards, ML-based risk estimates could support:
- Early identification of persistently underserved settings
- Prioritisation of outreach or technical assistance
- Strategic planning in resource-constrained contexts
However, model outputs should augment—not replace—expert judgment, and should never be used to justify withdrawal of support from disadvantaged settings.

**Limitations**
- The analysis is based on aggregated, country-level data and does not capture within-country heterogeneity.
- The study is predictive rather than causal.
- Reporting bias and temporal drift remain important challenges for operational use.

**Repository Structure**
notebooks/01_eda.ipynb: Data exploration and quality assessment
notebooks/02_risk_prediction.ipynb: Modeling and evaluation
notebooks/03_fairness_calibration.ipynb: Subgroup performance and calibration
results/: Tables and figures generated by the analysis

**About the Author**

I am a Preventive Medicine physician (MD) with an MPH, with research interests in health systems, digital health, and the responsible application of data-driven methods to improve population health and reduce inequities.

## References (selected)
1. World Health Organization & World Bank. Tracking Universal Health Coverage: Global Monitoring Report.
2. World Health Organization. Ethics and governance of artificial intelligence for health.
3. Morgenstern H. Ecologic studies in epidemiology. Annual Review of Public Health.

