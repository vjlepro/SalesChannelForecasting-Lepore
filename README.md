# Sales Channel Forecasting with MLForecast + LightGBM

A multi-channel sales forecasting model built with [MLForecast](https://github.com/Nixtla/mlforecast) from Nixtla and LightGBM. Forecasts monthly revenue across Direct, Retail, and Online channels using a lag-based regression approach — the same methodology used in production forecasting pipelines at mid-to-large companies.

---

## What This Solves

Most mid-size businesses need forward-looking sales visibility by channel to support budgeting, headcount planning, and inventory decisions. This model takes historical monthly sales data, learns the trend and momentum patterns within each channel, and projects 6 months forward — without requiring heavy seasonality or complex external inputs to get useful results.

---

## How the Model Works

Rather than fitting a traditional time series model like ARIMA directly, MLForecast converts the forecasting problem into a **supervised regression problem**:

- It generates **lag features** — the sales value from 1, 2, 3, and 6 months prior — and uses those as inputs
- It adds a **3-month rolling average** on the most recent lag to smooth short-term noise
- It extracts **month as a numeric feature** to give the model awareness of time position
- A **LightGBM regressor** then learns the relationship between those features and the next month's sales value

This approach works especially well for businesses without strong seasonality, where trend and recent momentum carry most of the predictive signal. A **Linear Regression** model is included as a baseline for comparison.

---

## Repo Structure

```
├── sales_channel_forecast.ipynb   # Main notebook — data, model, evaluation, charts
└── README.md
```

---

## Results

The notebook produces:

- **Forecast chart** — 6-month forward projections per channel, LightGBM vs Linear Regression
- **Cross-validation accuracy** — MAE and RMSE across 3 rolling time windows (no data leakage)
- **Feature importance chart** — which lag features drove the most predictive power in LightGBM

---

## Tech Stack

| Tool | Purpose |
|---|---|
| [MLForecast](https://github.com/Nixtla/mlforecast) | Time series to regression pipeline |
| [LightGBM](https://lightgbm.readthedocs.io/) | Primary forecasting model |
| scikit-learn LinearRegression | Baseline comparison model |
| Plotly | Interactive visualizations |
| pandas / numpy | Data wrangling |

---

## How to Run

**Option 1 — Google Colab (recommended, no install required)**

1. Upload `sales_channel_forecast.ipynb` to [colab.research.google.com](https://colab.research.google.com)
2. Run the first code cell to install dependencies
3. Run all remaining cells top to bottom

**Option 2 — Local Jupyter**

```bash
pip install mlforecast lightgbm plotly pandas numpy
jupyter notebook sales_channel_forecast.ipynb
```

---

## What's Next

With real data piped in, natural extensions include:

- **External regressors** — add pricing, marketing spend, or macro indicators as model inputs via `fcst.fit(df, X_df=exog_df)`
- **Hyperparameter tuning** — optimize LightGBM parameters with Optuna for lower error
- **Prediction intervals** — quantify forecast uncertainty with conformal prediction
- **SKU or region-level forecasting** — MLForecast scales to thousands of series with no code changes, just add rows with new `unique_id` values

---

## Background

Built as part of an ongoing analytics portfolio focused on production-ready forecasting for finance and revenue operations use cases. Methodology informed by 15+ years of analytics work across fintech, CPG, and sports and entertainment verticals.
