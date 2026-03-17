# Energy Consumption Forecasting

## Project Overview

This project builds a machine learning model to forecast hourly electricity consumption using historical energy demand data from the PJM Interconnection electricity market.

The goal is to demonstrate an end-to-end workflow for time series forecasting using feature engineering and machine learning models.

The analysis includes:

- time series exploration
- temporal feature engineering
- lag feature creation
- rolling statistics
- baseline comparison
- machine learning forecasting models
- feature importance analysis

---

## Dataset

Dataset: **PJM Hourly Energy Consumption**

The dataset contains hourly electricity consumption measured in megawatts.

Main variables:

- **Datetime** → timestamp of the observation
- **PJME_MW** → electricity consumption in megawatts

The dataset spans multiple years of hourly observations.

Source:  
PJM Interconnection LLC

---

## Project Workflow

### 1. Data Loading and Cleaning
The dataset is loaded and the datetime column is converted into a proper time index.

### 2. Exploratory Data Analysis
The time series is visualized to understand overall patterns and short-term variations.

Boxplots are used to analyze how energy consumption varies across:

- hour of the day
- day of the week
- month of the year

These visualizations reveal strong temporal patterns in electricity demand.

### 3. Feature Engineering

Several types of features are created to help the model learn temporal dynamics.

#### Temporal Features
- hour
- day of week
- month
- quarter
- day of year
- week of year

#### Lag Features
Lag variables capture previous observations of the target variable.

Examples:

- lag_1h → consumption one hour earlier
- lag_24h → consumption same hour previous day
- lag_7d → consumption same hour previous week

#### Rolling Statistics
Rolling window features capture recent trends:

- rolling_mean_24h
- rolling_std_24h
- rolling_mean_7d

---

## Models

Several models are compared:

1. **Naive Baseline**
   - predicts current consumption using the previous hour

2. **Linear Regression**
   - baseline machine learning model

3. **Random Forest Regressor**
   - main forecasting model

4. **Random Forest without lag_1h**
   - robustness check to evaluate dependency on the strongest lag feature

---

## Model Performance

| Model | MAE | RMSE | R² | MAPE |
|-----|-----|-----|-----|-----|
| Naive Baseline | 1070 | 1373 | 0.955 | 0.034 |
| Linear Regression | 969 | 1239 | 0.964 | 0.031 |
| Random Forest | **369** | **509** | **0.994** | **0.011** |
| Random Forest (without lag_1h) | 1329 | 1802 | 0.923 | 0.042 |

The Random Forest model achieves the best forecasting performance.

---

## Feature Importance

Feature importance analysis shows that short-term lag features are the most informative predictors.

The most important variables include:

- lag_1h
- hour of day
- rolling_mean_24h
- lag_24h

This confirms that recent historical consumption strongly influences short-term electricity demand.

---

## Results Visualization

The final visualization compares:

- actual energy consumption
- Random Forest predictions
- predictions without lag_1h

This helps illustrate how the model tracks real demand patterns over time.

---

## Conclusion

This project demonstrates how machine learning can be applied to time series forecasting problems in the energy sector.

Key findings:

- electricity consumption shows strong temporal patterns
- lag features are extremely informative for short-term forecasting
- Random Forest significantly outperforms linear models
- removing the strongest lag reduces performance but still produces reasonable forecasts

These techniques can be applied in real-world scenarios such as:

- energy demand planning
- grid management
- load forecasting
- infrastructure optimization

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Joblib

---

## Author: Costanza Pizzi

Data Science portfolio project focused on time series forecasting and feature engineering.
