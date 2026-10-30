# Taxi Demand Prediction

Predicts how many taxi pickups will happen in each New York City zone in the next 30 minutes (time-series regression).

## Data
- NYC TLC yellow taxi trip records, January 2024 (2,964,624 trips)
- Kept the 30 busiest pickup zones (2,419,051 trips)
- Counted pickups per zone per 30-minute slot: 44,640 rows, 43,200 after building features

## Method
- Features: slot of day, day of week, weekend flag, pickups in the previous 3 slots, pickups at the same time yesterday, average of the last 4 slots, zone average
- Split by time: train on Jan 2-24 (33,120 rows), test on Jan 25-31 (10,080 rows)
- Models: two simple baselines, Linear Regression, XGBoost
- Metrics: MAE, and MAPE (only for slots with 10 or more real pickups)

## Results

| Method | MAE | MAPE |
|---|---|---|
| Baseline: same time yesterday | 17.64 | 40.6% |
| Baseline: previous slot | 12.00 | 25.8% |
| Linear Regression | 11.01 | 23.5% |
| XGBoost | 9.21 | 19.1% |

Best model: XGBoost, about 23% lower MAE than the best baseline.

## Limitations
- One month of data, and a one-week test set
- Only the 30 busiest zones
- No weather, holiday or event features
- XGBoost settings not tuned

## Tools
Python, pandas, numpy, scikit-learn, XGBoost, Google Colab
