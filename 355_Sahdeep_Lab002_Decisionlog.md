# Lab 02 — Decision Log

## Ingestion
- Source: seaborn.load_dataset('titanic') → exported to titanic.csv
- Timestamp (IST): 2025-08-17, 16:57
- Environment: pandas==2.0.3, seaborn==0.13.0, missingno==0.5.2, numpy==1.25.2

## Missing Values
- Strategy:
- Numeric → median (why: robust to outliers and skewness, which is present in columns like 'age', preserving the central tendency better than the mean.)
- Categorical → mode (why: provides the most frequent category, which is a simple and effective way to fill missing values without introducing new ones. It maintains the original data distribution for nominal variables.)
- Columns imputed & flags created:
- age (median), age_was_missing added
- embarked (mode), embarked_was_missing added
- deck (mode), deck_was_missing added
- embark_town (mode), embark_town_was_missing added
- alone (mode), alone_was_missing added

## Outliers (Fare)
- Method: Log1p transform
- Rationale: The 'fare' column is heavily skewed to the right due to a small number of very expensive tickets. A log transformation compresses the range of these high values, normalizing the distribution and making it more suitable for many statistical and machine learning models that assume normally distributed data. `log1p` is used to gracefully handle a potential `0` value.
- Alternatives considered:
- IQR clip: Simple but can distort the original distribution by capping values at an arbitrary threshold.
- Winsorize: Similar to clipping but replaces outliers with a chosen percentile value, which can be less intuitive.
- Removal: Reduces the sample size, which could lead to loss of valuable information and a less generalizable model, especially since only a few values are extremely high.

## Validation
- Ran `df.info()` and `df.describe()` after cleaning to confirm no missing values remained.
- Ensured all flag columns were correctly created as booleans.
- Confirmed the data types were as expected after imputation and transformation.

## Reproducibility Notes
- All data cleaning steps are implemented as a series of deterministic operations within the Jupyter notebook.
- The `decision_log.md` documents the exact methods and parameters used, ensuring that the preprocessing can be replicated by others.
- The output `355_Sahdeep_Lab002_clean_v1.csv` is a direct result of these documented steps.