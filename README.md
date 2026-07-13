# unusual-coastal-trash-ml
Machine learning project predicting high-unusual coastal debris cleanup events using Python and scikit-learn.

# Predicting High-Unusual Coastal Debris Events Using Machine Learning

## Overview

In this project, I used machine learning to predict coastal cleanup events with unusually high shares of nonstandard debris. I converted cleanup-level data into a supervised binary classification problem and compared Logistic Regression, Random Forest, and Gradient Boosting models.

The main goal was to predict whether a cleanup event would be classified as a `high_unusual_event`, defined as an event in the top 25% of unusual debris share.

## Research Question

Can cleanup-level information such as time, location, cleanup type, and cleanup effort predict whether a coastal cleanup event has a high share of unusual debris?

## Data

The unit of analysis is one cleanup event. The full dataset comes from Ocean Conservancy's 2015-2026 cleanup reports. Because item categories and reporting structures changed across years, I also built a cleaner 2023–2025 model using more consistent and recent-year data.

## Target Variable

The target variable was constructed as:

```text
unusual_share = unusual_debris_count / total_items_collected

high_unusual_event = 1 if unusual_share is in the top 25%
high_unusual_event = 0 otherwise
