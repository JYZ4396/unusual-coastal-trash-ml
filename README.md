# Predicting High-Unusual Coastal Debris Events Using Machine Learning

## Overview

In this project, I used machine learning to predict coastal cleanup events with unusually high shares of nonstandard debris. I converted cleanup-level data into a supervised binary classification problem and compared Logistic Regression, Random Forest, and Gradient Boosting models.

The main goal was to predict whether a cleanup event would be classified as a `high_unusual_event`, defined as an event in the top 25% of unusual debris share.

## Research Question

Can cleanup-level information such as time, location, cleanup type, and cleanup effort predict whether a coastal cleanup event has a high share of unusual debris?

## Data

The unit of analysis is one cleanup event. The full dataset covers cleanup records from 2015 to 2026.

Because item categories and reporting structures changed across years, I first trained models on the full 2015–2026 dataset, then built a cleaner 2023–2025 model using recent years with more consistent category structures.


## Target Variable

For each cleanup event, I calculated the share of unusual debris:

```text
unusual_share = unusual_debris_count / total_items_collected
```

Then I defined the binary target variable:

```text
high_unusual_event = 1 if unusual_share is in the top 25%
high_unusual_event = 0 otherwise
```

This makes the project a supervised binary classification problem.

## Methods

This project includes:

- Data cleaning and column standardization across yearly files
- Exploratory data analysis
- Target variable construction
- Logistic Regression baseline model
- Random Forest model
- Gradient Boosting model
- Model comparison using classification metrics
- No-year robustness check
- Permutation feature importance analysis
- A cleaner 2023–2025 model for more interpretable results

## Models

Three models were tested:

1. **Logistic Regression**  
   Used as an interpretable baseline model.

2. **Random Forest**  
   Used to capture nonlinear relationships and feature interactions.

3. **Gradient Boosting**  
   Used as a more flexible tree-based model. This was the best-performing model in both the full 2015–2026 analysis and the clean 2023–2025 analysis.

## Evaluation Metrics

Because high-unusual-debris events make up only about 25% of the dataset, accuracy alone is not enough. I evaluated the models using:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- PR-AUC

PR-AUC and recall are especially important because the project focuses on identifying the positive class: high-unusual-debris events.

## Key Results

In the full 2015–2026 model, Gradient Boosting performed best, with:

- ROC-AUC: approximately 0.842
- PR-AUC: approximately 0.638

However, permutation feature importance showed that `year` was the dominant predictor. This raised a concern that the model may have learned changes in reporting structure or item category definitions across years.

To address this, I built a cleaner 2023–2025 model. In this model, Gradient Boosting again performed best, with:

- ROC-AUC: approximately 0.752
- PR-AUC: approximately 0.547

Although the clean model had lower performance than the full model, it was more interpretable because it reduced the influence of cross-year category changes.

## Main Findings

The clean 2023–2025 model suggests that geographic variables are the strongest predictors of high-unusual-debris events.

The most important features were:

- `zone_name`
- `Longitude`
- `Latitude`
- `month`
- `state_name`

This suggests that high-unusual-debris events are spatially uneven and strongly related to local cleanup context.

The broad `hurricane_season` variable had very low feature importance. This does not mean storms are irrelevant. Instead, it suggests that a simple hurricane-season indicator is too broad to capture actual storm exposure.

## Limitations

This project identifies predictive associations, not causal effects.

Main limitations include:

- The definition of unusual debris is researcher-defined.
- Item categories changed across years.
- 2026 is only a partial year.
- Cleanup records may reflect volunteer activity and reporting behavior.
- The hurricane-season variable does not capture actual storm exposure, storm severity, storm track, or days since storm.

## Future Work

Future work could improve this project by adding actual storm-event data, such as:

- Hurricane landfall dates
- Storm tracks
- Wind speed
- Rainfall
- Storm surge
- Days since storm

Another extension would be to build regional models, such as a Florida-specific model, or to use clustering and anomaly detection to identify unusual debris patterns without manually defining the target variable.

## Repository Structure

```text
notebooks/   Jupyter notebook for data cleaning, EDA, and modeling
figures/     Key visualizations used in the report
reports/     Full project report PDF
data/        Data source notes
```

## Tools Used

- Python
- pandas
- NumPy
- scikit-learn
- matplotlib
- Jupyter Notebook
- Google Docs for report writing

## Project Status

The report and figures are being finalized. The cleaned notebook will be uploaded after final code review.
