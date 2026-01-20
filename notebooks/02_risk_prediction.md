# Risk Prediction: Low UHC Service Coverage

## Objective
This analysis frames low essential health service coverage as a risk prediction problem.
Using population-level indicators, we aim to identify country–year settings at higher risk
of low UHC service coverage.

The primary goal is not algorithmic novelty, but a transparent and evaluation-focused workflow
that reflects how such models could be used to support public health prioritisation.

---

## Outcome definition (binary label)
The outcome is derived from the UHC Service Coverage Index (SDG 3.8.1).

To obtain a policy-relevant binary target, we define:
- **Low coverage (y = 1):** country–year observations in the **lowest quartile** of UHC index within each year
- **Not low coverage (y = 0):** all remaining observations

This year-specific definition reduces sensitivity to global secular trends and focuses the model on
relative under-coverage within each time period.

---

## Data and features
The modeling dataset is constructed at the country–year level and includes:
- Health system capacity proxies (e.g., health expenditure, workforce indicators where available)
- Socioeconomic indicators (e.g., GDP per capita, education proxies)
- Demographic and epidemiological context indicators (e.g., life expectancy, under-5 mortality)

Only publicly available, aggregated indicators are used.

---

## Train–test split (temporal)
To reflect realistic forecasting and reduce leakage, we adopt a temporal split:
- **Training set:** earlier years (e.g., ≤ 2016)
- **Test set:** later years (e.g., ≥ 2017)

This choice mirrors the real-world use case where models trained on historical data are applied to
future periods for planning and prioritisation.

---

## Models
We compare two commonly used models in applied public health ML:

1. **Logistic Regression**
- Baseline, interpretable
- Useful for understanding directionality of associations (with caution)

2. **Random Forest**
- Non-linear baseline
- Captures interactions and non-linearities without strong parametric assumptions

These models provide a practical balance between performance and interpretability.

---

## Evaluation metrics
Because low coverage is defined as the bottom quartile, class imbalance is expected.
We therefore prioritise:

- **AUROC** (discrimination)
- **AUPRC** (performance under imbalance; emphasises positive class utility)
- **Recall for low-coverage settings** (public health relevance; missing underserved settings is costly)

In addition, confusion matrices are reported for transparent error accounting.

---

## Thresholding and public health utility
For operational relevance, classification thresholds should reflect programme priorities.
Where appropriate, we consider thresholds that prioritise:
- Higher recall for low coverage (minimising false negatives)
- Acceptable precision (avoiding an unmanageable number of false positives)

Model outputs are best interpreted as **risk scores** supporting human decision-making,
rather than deterministic classifications.

---

## Interpretability and feature patterns (associative, not causal)
For transparency, we examine:
- Logistic regression coefficients (standardised where applicable)
- Random forest feature importances

These outputs are interpreted as predictive associations, not causal effects.
They are used to check face validity and identify potential data artifacts.

---

## Error analysis
We place particular emphasis on false negatives:
- Country–year settings with low coverage that are not flagged as high risk

This is important because such errors would correspond to missed opportunities for early support
in real-world public health workflows.

Where feasible, we summarise common characteristics of missed cases (e.g., missingness, regional patterns).

---

## Expected outputs
This step produces (to be completed once code is run):
- Overall performance table (AUROC, AUPRC, recall) for each model
- Confusion matrix summaries
- A ranked list of predictive features (interpretable patterns)
- A short error analysis highlighting false-negative cases

---

## Illustrative code (for reproducibility)
The following code snippet shows the intended workflow (to be run in a Python environment):

```python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import roc_auc_score, average_precision_score, confusion_matrix

# Load processed dataset (placeholder path)
df = pd.read_csv("data/processed/uhc_ml_dataset.csv")

# Example: year-specific bottom quartile labeling
df["low_uhc"] = df.groupby("year")["uhc_index"].transform(lambda x: x <= x.quantile(0.25)).astype(int)

# Temporal split (example cut)
train = df[df["year"] <= 2016].copy()
test  = df[df["year"] >= 2017].copy()

feature_cols = [c for c in df.columns if c not in ["country", "year", "uhc_index", "low_uhc"]]
X_train, y_train = train[feature_cols], train["low_uhc"]
X_test, y_test   = test[feature_cols], test["low_uhc"]

# Logistic regression pipeline
lr = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("scaler", StandardScaler()),
    ("model", LogisticRegression(max_iter=2000))
])
lr.fit(X_train, y_train)
p_lr = lr.predict_proba(X_test)[:, 1]

# Random forest pipeline
rf = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("model", RandomForestClassifier(n_estimators=300, random_state=42))
])
rf.fit(X_train, y_train)
p_rf = rf.predict_proba(X_test)[:, 1]

# Metrics
def report(y_true, p):
    auroc = roc_auc_score(y_true, p)
    auprc = average_precision_score(y_true, p)
    y_hat = (p >= 0.5).astype(int)
    cm = confusion_matrix(y_true, y_hat)
    return auroc, auprc, cm

print("LR:", report(y_test, p_lr))
print("RF:", report(y_test, p_rf))

---

## Summary
This step demonstrates how population-level indicators can be used to construct
transparent and policy-relevant risk prediction models for low health service coverage.

Model evaluation prioritises recall for underserved settings and explicit error analysis,
reflecting public health rather than purely technical objectives.

