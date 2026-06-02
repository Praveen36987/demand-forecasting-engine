# 🔮 Demand Forecasting Engine
### Python Analytics Portfolio Project | Store Item Demand Forecasting

---

## 📌 Problem Statement

A retail business operating 10 stores across 50 product lines has no reliable
way to predict future demand. Without accurate forecasts, the business faces two
costly outcomes — overstocking (dead inventory) or understocking (lost sales).

This project builds and compares three forecasting models to predict daily sales
90-365 days ahead, identifies the best performing approach, and explains why it
wins using data.

> **Key finding:** Prophet outperformed ARIMA by 79% and XGBoost by 57%
> on this dataset — proving that seasonality-aware models are essential for
> retail demand forecasting.

---

## 🎯 Project Objectives

- Explore 5 years of daily sales data across 10 stores and 50 items
- Engineer time-based features that teach models about seasonality
- Build 3 forecasting models — ARIMA, Prophet and XGBoost
- Compare model performance using MAPE
- Identify the best model and explain the business recommendation

---

## 🗃️ Dataset

| Property | Detail |
|---|---|
| Source | [Store Item Demand Forecasting — Kaggle](https://www.kaggle.com/competitions/demand-forecasting-kernels-only) |
| Rows | 913,000 daily records |
| Columns | date, store, item, sales |
| Period | 2013-01-01 to 2017-12-31 |
| Stores | 10 |
| Items | 50 |

---

## 🛠️ Tools & Libraries

| Tool | Usage |
|---|---|
| pandas, numpy | Data manipulation and feature engineering |
| matplotlib, seaborn | Visualisation |
| statsmodels ARIMA | Statistical baseline model |
| Prophet | Seasonality-aware forecasting |
| XGBoost | ML-based forecasting |
| sklearn | Model evaluation (MAPE, RMSE) |

---

## 📊 EDA Findings

### Finding 1 — Strong upward trend
Total daily sales grew from ~13,000 in January 2013 to peaks of ~45,000 by
mid 2017. The business is growing year on year — any forecast model must
capture this trend.

### Finding 2 — Weekly seasonality is dominant
Sunday sales average 62.1 units per store-item vs Monday's 41.4 — a **50%
swing** within a single week. This pattern repeats consistently across all
5 years.

### Finding 3 — Clear yearly seasonality
August peaks at 67 average units while January dips to 35 — a **91% seasonal
swing** across the year. Summer drives significantly higher demand than winter.

---

## 🔧 Feature Engineering

6 features extracted from the date column to give models temporal signals:

| Feature | What it captures |
|---|---|
| day_of_week | Weekly pattern (0=Mon, 6=Sun) |
| month | Monthly seasonality |
| year | Long term growth trend |
| quarter | Broad seasonal buckets |
| week_of_year | Fine-grained seasonal position |
| is_weekend | Binary weekend flag |

---

## 🤖 Model Results

| Model | MAPE | vs Baseline |
|---|---|---|
| ARIMA(7,1,0) | 26.66% | Baseline |
| XGBoost | 13.04% | 51% better |
| **Prophet** | **5.64%** | **79% better** |

### Why Prophet won
Prophet was designed specifically for business time series with multiple
seasonality patterns. It automatically detected:
- **Trend:** steady growth from 22K to 32K daily sales
- **Weekly:** Sunday +4,500 above average, Monday -4,500 below average
- **Yearly:** July peak at +7,500, December/January trough at -7,500

### Why ARIMA underperformed
ARIMA has no built-in seasonality awareness. When forecasting 365 days ahead
it regresses to the mean — producing a flat line that misses all seasonal
variation completely.

### XGBoost's unique advantage
Despite a higher MAPE than Prophet on aggregated sales, XGBoost operated at
**store × item level** (500 unique combinations vs Prophet's single aggregate).
Feature importance revealed item identity drives 37% of forecast accuracy —
making XGBoost the right choice when granular predictions are needed.

---

## 💡 Business Recommendations

| Priority | Recommendation |
|---|---|
| Forecasting engine | Deploy Prophet for company-wide demand planning |
| Granular planning | Use XGBoost for store-item level inventory decisions |
| Inventory timing | Stock up from May — sales peak in July/August |
| Staffing | Schedule 50% more weekend staff vs Monday across all stores |
| Retirement | Retire any manual forecasting — ARIMA's 26.66% error is too costly |

---

## 📁 Project Structure

```
demand-forecasting-project/
├── README.md
├── data/
│   └── data_source.md
├── notebooks/
│   └── demand_forecasting.ipynb
└── results/
    └── screenshots/
```

---

## 🚀 How To Run

1. Download dataset from Kaggle (link above)
2. Install dependencies: `pip install pandas numpy matplotlib seaborn statsmodels prophet xgboost scikit-learn`
3. Open `notebooks/demand_forecasting.ipynb`
4. Run all cells in order

---

*Built as part of a BI analytics portfolio. Demonstrates EDA, feature
engineering, statistical modelling (ARIMA), seasonality-aware forecasting
(Prophet) and ML-based forecasting (XGBoost) with full model comparison.*
