# Air-Kuality-detector
# Beijing PM2.5 Prediction with Machine Learning

## Project Overview
This project uses **Random Forest Regression** to predict PM2.5 concentration based on multi-site air quality and meteorological data from Beijing.

It aligns with **SDG 11 (Sustainable Cities and Communities)** and **SDG 3 (Good Health and Well-being)**.

## Dataset
- **Name**: Beijing Multi-Site Air Quality Dataset
- **Source**: Online public dataset (Kaggle / similar structured air quality data)
- **Original Size**: > 400,000 rows, 15+ columns
- **State**: Uncleaned structured data (as required)
- **Target Variable**: `PM2.5`
- **Selected Features** (14 features):
  - PM10, SO2, NO2, CO, O3
  - TEMP, PRES, DEWP, RAIN, WSPM
  - year, month, day, hour

**Feature Descriptions:**
- **PM10** – Particulate Matter (≤10 μm), mainly from dust and combustion
- **SO2** – Sulfur Dioxide, from coal burning and industrial emissions
- **NO2** – Nitrogen Dioxide, mainly from vehicle exhaust
- **CO** – Carbon Monoxide, indicator of incomplete combustion
- **O3** – Ozone, secondary pollutant formed by photochemical reactions

### Data Cleaning Steps
1. Removed rows where `PM2.5` was missing
2. Performed station-wise linear interpolation for numeric features
3. Filled remaining missing values (e.g., NO2) using station median
4. Handled categorical feature `wd` (wind direction) with mode filling
5. Final clean dataset: 412,029 rows with **zero missing values**

## Model
- **Algorithm**: Random Forest Regressor
- **Parameters**:
  - `n_estimators=50`
  - `max_depth=20`
  - `random_state=42`
- **Train/Test Split**: 80% / 20%
  - Training set: 329,623 samples
  - Test set: 82,406 samples

## Model Performance
| Metric | Value |
|--------|-------|
| MAE    | 10.48 |
| RMSE   | 17.68 |
| **R²** | **0.9520** |

The model explains approximately **95.2%** of the variance in PM2.5 levels.

## Feature Importance (Top 5)
1. **PM10** (0.806) – Strongly correlated with PM2.5
2. **CO** (0.098) – Indicator of combustion sources
3. **DEWP** (0.018) – Dew point temperature (humidity)
4. **SO2** (0.013) – Precursor of secondary sulfate aerosols
5. **TEMP** (0.010) – Temperature

### Selected Features for Detailed Discussion
- **PM10**: Highly correlated with PM2.5 due to shared emission sources and atmospheric behavior.
- **CO**: Represents incomplete combustion (traffic and industry), a major source of PM2.5.
- **SO2**: Contributes to secondary aerosol formation (sulfate particles) that form part of PM2.5.

## Files in this Repository
