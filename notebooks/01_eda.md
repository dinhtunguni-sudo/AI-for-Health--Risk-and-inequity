# Exploratory Data Analysis (EDA)

## Objective
This exploratory analysis examines the Universal Health Coverage (UHC) Service Coverage Index
to understand its distribution, temporal trends, and data completeness prior to predictive modeling.

The unit of analysis is country-year.

---

## Data source
- Universal Health Coverage (UHC) Service Coverage Index  
  Source: Our World in Data (WHO / World Bank)

---

## Data loading (illustrative code)

```python
import pandas as pd

uhc_url = "https://raw.githubusercontent.com/owid/owid-datasets/master/datasets/UHC%20Service%20Coverage%20Index/UHC%20Service%20Coverage%20Index.csv"
uhc = pd.read_csv(uhc_url)

---

## Initial data checks
The dataset consists of country–year observations with the following core variables:
- Country name
- Year
- UHC Service Coverage Index

Preliminary inspection confirms that the index is reported for multiple years across most countries,
with varying degrees of completeness depending on time period and region.

---

## Distribution of the UHC Service Coverage Index
The distribution of the UHC Service Coverage Index shows substantial heterogeneity across settings.
Lower values are predominantly observed in lower-income countries, while higher-income settings
cluster toward higher coverage levels.

This variability supports framing the modeling task as identifying country–year settings
at risk of persistently low service coverage.

---

## Temporal considerations
Coverage levels change over time as a result of health system investments, policy reforms,
and broader socioeconomic development. As a result, any predictive modeling should respect
the temporal structure of the data.

Subsequent analyses therefore adopt a temporal train–test split to better reflect
real-world forecasting and decision-making scenarios.

---

## Limitations of this exploratory analysis
This exploratory analysis is descriptive in nature and based on aggregated, country-level data.
Findings should therefore be interpreted at the population level and do not capture
within-country inequalities.

These limitations are considered explicitly in subsequent modeling and interpretation steps.

