# Rossmann Demand Forecasting

## Overview

This project focuses on retail demand forecasting using the Rossmann Store Sales dataset.

The objective is to predict daily store sales using historical sales patterns, promotional information, store characteristics, and calendar-based features.

## Dataset

- 1,017,209 training records
- 1,115 stores
- Training period: January 2013 – July 2015
- Test period: August 2015 – September 2015

## Methodology

### Data Preparation
- Data quality and missing-value analysis
- Duplicate detection
- Train and store data merging
- Date-based feature engineering
- Time-based train/validation split

### Feature Engineering

Calendar features:
- Year
- Month
- Day
- Week of Year
- Quarter
- Day of Week
- Weekend indicator

Historical sales features:
- Sales Lag 1
- Sales Lag 7
- Sales Lag 14
- 7-day rolling average
- 14-day rolling average
- 28-day rolling average

Store and promotion features:
- Store Type
- Assortment
- Competition Distance
- Promo
- Promo2
- State Holiday
- School Holiday

## Model

CatBoost Regressor was used for demand forecasting.

A baseline model was first trained using store, promotion, calendar, and store characteristics.

A second model incorporated historical sales lag and rolling-window features.

## Results

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline CatBoost | 658.37 | 984.85 | 0.9301 |
| CatBoost + Lag/Rolling | **475.96** | **740.65** | **0.9605** |

The addition of historical sales features reduced RMSE by approximately **24.8%**.

## Feature Importance

The most influential features were:

1. Open
2. Promo
3. Sales Rolling 28
4. Sales Lag 14
5. Sales Lag 1
6. Sales Rolling 7
7. Day
8. Sales Lag 7

These results show the importance of store operating status, promotions, and historical sales patterns in demand forecasting.

## Validation Strategy

A chronological validation strategy was used to avoid data leakage.

- Training: January 1, 2013 – June 19, 2015
- Validation: June 20, 2015 – July 31, 2015

The final model was also used to generate predictions for the 41,088 records in the test dataset.

## Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- CatBoost
- Scikit-learn
- Google Colab

Key Takeaway

Historical demand patterns provided substantial predictive value. Adding lag and rolling-window features improved the CatBoost model from an RMSE of 984.85 to 740.65 while increasing R² from 0.9301 to 0.9605.
## Project Structure

```text
rossmann-demand-forecasting/
│
├── Demand_Forecasting_Rossmann.ipynb
├── README.md
└── .gitignore
