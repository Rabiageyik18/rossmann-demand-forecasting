Rossmann Demand Forecasting

Overview

This project focuses on daily retail demand forecasting using the Rossmann Store Sales dataset.

The objective is to predict store-level daily sales using historical sales patterns, promotional information, store characteristics, and calendar features.

Dataset

1,017,209 training records

1,115 stores

Training period: 2013-01-01 – 2015-07-31

Test period: 2015-08-01 – 2015-09-17

Test records: 41,088

Approach

Data Preparation

Missing-value and duplicate analysis

Merging transaction data with store metadata

Date and calendar feature engineering

Chronological train/validation split to avoid data leakage

Feature Engineering

Calendar features

Year

Month

Day

Week of Year

Quarter

Day of Week

Weekend indicator

Historical sales features

Sales Lag 1

Sales Lag 7

Sales Lag 14

7-day rolling average

14-day rolling average

28-day rolling average

Business/store features

Store Type

Assortment

Competition Distance

Promo

Promo2

State Holiday

School Holiday

Modeling

A CatBoost Regressor was used as the main forecasting model.

Two models were evaluated:

Baseline CatBoost using store, promotion, calendar, and store characteristics.

CatBoost + Lag/Rolling Features incorporating historical sales behavior.

Validation was performed chronologically:

Training: 2013-01-01 → 2015-06-19

Validation: 2015-06-20 → 2015-07-31

Results

Model

MAE

RMSE

R²

Baseline CatBoost

658.37

984.85

0.9301

CatBoost + Lag/Rolling

475.96

740.65

0.9605

Adding lag and rolling-window features reduced RMSE by approximately 24.8% and improved R² from 0.9301 to 0.9605.



Actual vs Predicted Sales

The validation predictions closely follow the daily sales pattern, including weekly fluctuations and major peaks.



Feature Importance

The strongest model features were:

Open

Promo

Sales_Rolling_28

Sales_Lag_14

Sales_Lag_1

Sales_Rolling_7

Day

Sales_Lag_7



The results highlight the importance of store operating status, promotions, and historical demand patterns.

Test Forecast

The final model generated predictions for all 41,088 test records.

The predictions were exported to:

submission.csv

Technologies

Python

Pandas

NumPy

Matplotlib

Scikit-learn

CatBoost

Google Colab

Repository Structure

rossmann-demand-forecasting/
│
├── Demand_Forecasting_Rossmann.ipynb
├── README.md
├── feature_importance.png
├── actual_vs_predicted.png
├── model_comparison.png
└── .gitignore

Key Takeaway

Historical demand information substantially improved forecasting performance. The final CatBoost model achieved RMSE 740.65, MAE 475.96, and R² 0.9605 on the time-based validation set.
