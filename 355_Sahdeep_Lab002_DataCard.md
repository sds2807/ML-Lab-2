# Data Card — Titanic (Clean_v1)

## Overview
- Records: 891
- Features: 18
- Target (if any): N/A for this lab

## Schema (post-clean)
- age: float64 (median-imputed, age_was_missing added)
- embarked: object (mode-imputed, embarked_was_missing added)
- deck: object (mode-imputed, deck_was_missing added)
- embark_town: object (mode-imputed, embark_town_was_missing added)
- alone: bool (mode-imputed, alone_was_missing added)
- fare: float64 (original, used for log transformation)
- fare_log1p: float64 (log1p transformed)
- All other columns are unchanged.

## Integrity
- Missing handled: yes (age, embarked, deck, embark_town, alone)
- Duplicates: 0
- Types checked: yes (no type conversions were necessary beyond the boolean flags)

## Visuals
- NA Heatmap:

*The heatmap above shows that all missing values have been successfully handled.*

- Fare Distribution (after treatment):

*This plot shows the 'fare' distribution is more symmetrical after the log1p transformation, reducing the skewness caused by high-value outliers.*

## Known Limitations / Bias Note
- Potential bias: The dataset is imbalanced with respect to 'survived' (target for later labs), and some features like 'pclass' and 'sex' are highly correlated with survival.
- Impact on generalization: Imputing values might introduce a slight bias towards the central tendency of the data, which may not accurately reflect the true, unobserved values. The log transformation, while useful for modeling, changes the scale and interpretability of the `fare` feature.