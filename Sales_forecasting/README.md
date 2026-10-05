# Sales & Demand Forecasting for Retail Businesses

## Project Overview

This project analyzes historical retail sales data and builds a **monthly sales forecasting model** to help businesses plan inventory, staffing, cash flow, and marketing activities.

The project uses the **Superstore retail dataset** and follows a complete machine-learning/time-series workflow:

- Data loading and inspection
- Data cleaning and validation
- Monthly sales aggregation
- Exploratory analysis and visualization
- Time-series decomposition
- Feature engineering
- Model training
- Model comparison
- Forecast error analysis
- 12-month future sales forecasting
- Business recommendations

> **Note:** The notebook is the primary source of truth for the implementation and results.

---

## Project Title

**Sales & Demand Forecasting for Retail Businesses**

---

## Problem Statement

Retail businesses need reliable demand estimates to make better operational decisions. Poor forecasting can lead to:

- Overstocking
- Stock shortages
- Inefficient staffing
- Poor cash-flow planning
- Missed sales opportunities

This project uses historical sales data to identify patterns and generate a **12-month sales forecast**.

---

## Objectives

1. Analyze historical retail sales performance.
2. Convert order-level data into monthly sales data.
3. Identify trends and seasonal patterns.
4. Train multiple forecasting approaches.
5. Compare models using MAE, RMSE, and MAPE.
6. Select the best-performing model.
7. Forecast sales for the next 12 months.
8. Translate the forecast into practical business recommendations.

---

## Dataset

The project uses a **Superstore retail sales dataset** loaded from:

```text
data/superstore.csv
```

The dataset contains **9,994 records and 21 columns**.

Important fields include:

| Column | Description |
|---|---|
| `Order ID` | Unique order identifier |
| `Order Date` | Date when the order was placed |
| `Ship Date` | Shipping date |
| `Ship Mode` | Shipping method |
| `Customer ID` | Customer identifier |
| `Segment` | Customer segment |
| `City` | Customer city |
| `State` | Customer state |
| `Region` | Sales region |
| `Category` | Product category |
| `Sub-Category` | Product sub-category |
| `Product Name` | Product name |
| `Sales` | Sales amount |
| `Quantity` | Quantity ordered |
| `Discount` | Discount applied |
| `Profit` | Profit generated |

The notebook converts `Order Date` into a datetime value and uses `Sales` as the forecasting target.

---

## Data Preprocessing

The preprocessing workflow includes:

1. Loading the CSV dataset.
2. Inspecting shape, data types, and sample records.
3. Converting `Order Date` into datetime format.
4. Checking duplicate records.
5. Checking missing values in the forecasting fields.
6. Removing duplicate records.
7. Removing rows with missing `Order Date` or `Sales`.
8. Keeping observations where `Sales > 0`.
9. Aggregating sales at a monthly level.

The dataset initially contains **9,994 rows**, and the notebook reports **0 duplicate records** and no missing values in `Order Date` and `Sales`; therefore, no rows were removed during the cleaning checks.

---

## Exploratory Data Analysis

The project analyzes monthly sales behavior using visualizations and time-series decomposition.

The notebook identifies **48 months of sales history**.

Key analysis areas include:

- Monthly sales trends
- Historical sales visualization
- Seasonal decomposition
- Actual vs predicted sales
- Forecast errors
- Future forecast with an estimated range

---

## Feature Engineering

The forecasting workflow creates time-based features from the monthly index.

These features allow the Linear Regression model to learn the relationship between time and sales.

The project also preserves the monthly structure of the data so that the forecasting problem remains chronological.

---

## Models Used

Three forecasting approaches are trained and compared:

### 1. Seasonal Naive

Uses the previous 12 months as the seasonal reference for prediction.

### 2. Linear Regression

A regression model trained using time-based features to estimate monthly sales.

### 3. Holt-Winters

An Exponential Smoothing model with:

- Additive trend
- Additive seasonality
- 12-month seasonal period

---

## Model Evaluation

The models are evaluated using:

### MAE — Mean Absolute Error

Measures the average absolute difference between actual and predicted sales.

### RMSE — Root Mean Squared Error

Measures prediction error while giving greater weight to larger errors.

### MAPE — Mean Absolute Percentage Error

Measures average prediction error as a percentage.

The notebook selects the model with the **lowest RMSE**.

### Best Model

**Linear Regression**

- RMSE: approximately **14,399**
- MAPE: approximately **21.7%**

The notebook therefore uses Linear Regression for the final 12-month forecast.

---

## Forecast Results

The final model produces a forecast for the next **12 months**.

According to the notebook output:

| Metric | Result |
|---|---:|
| Model used | Linear Regression |
| Typical MAPE | ~21.7% |
| Last 12 months sales | $733,215 |
| Next 12 months forecast | $795,694 |
| Expected change | +8.5% |
| Strongest forecast month | November 2018 |
| Strongest forecast value | $86,373 |
| Weakest forecast month | February 2018 |
| Weakest forecast value | $51,630 |
| Top forecast months | November, September, December |

The forecast values are also saved to:

```text
outputs/forecast.csv
```

---

## Error Analysis

The project performs month-by-month error analysis for the selected model.

The notebook reports:

- Average error/bias: **7,244**
- Forecast tendency: **under-forecast**
- Worst month by absolute error: **January 2017**
- MAPE: **21.7%**

The project also generates an error visualization:

```text
outputs/error_by_month.png
```

and an actual-vs-predicted visualization:

```text
outputs/actual_vs_pred.png
```

---

## Business Recommendations

The forecast can be used to support practical retail decisions.

### Inventory

Increase inventory planning approximately **6–8 weeks before the strongest forecast months** and avoid excessive stock before the weakest month.

### Staffing

Plan additional staff or shifts around the strongest forecast periods.

### Cash Flow

Maintain sufficient cash reserves for weaker periods and for purchasing inventory before peak demand.

### Marketing

Use promotional campaigns during weaker demand periods to help smooth sales.

### Planning

The forecast range can be used for conservative and optimistic planning scenarios.

---

## Project Workflow

```text
Raw Superstore Data
        |
        v
Data Loading
        |
        v
Data Inspection
        |
        v
Data Cleaning
        |
        v
Date Conversion
        |
        v
Monthly Sales Aggregation
        |
        v
Exploratory Data Analysis
        |
        v
Seasonal Decomposition
        |
        v
Feature Engineering
        |
        v
Train Forecasting Models
        |
        +-------------------+
        |                   |
        v                   v
 Seasonal Naive      Linear Regression
        |                   |
        +---------+---------+
                  |
                  v
            Holt-Winters
                  |
                  v
          Model Evaluation
                  |
                  v
        Select Best Model
                  |
                  v
        12-Month Forecast
                  |
                  v
       Business Recommendations
```

---

## Project Structure

```text
sales-demand-forecasting/
│
├── data/
│   └── superstore.csv
│
├── outputs/
│   ├── forecast.csv
│   ├── forecast.png
│   ├── actual_vs_pred.png
│   └── error_by_month.png
│
├── ML_project.ipynb
├── requirements.txt
└── README.md
```

---

## Technologies Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Statsmodels

The provided `requirements.txt` contains:

```text
pandas
numpy
matplotlib
scikit-learn
statsmodels
jupyternotebook
```

---

## Installation

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd sales-demand-forecasting
```

### 2. Create a virtual environment (optional)

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Start Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
ML_project.ipynb
```

---

## How to Run

1. Place the dataset at:
   ```text
   data/superstore.csv
   ```
2. Install the required Python packages.
3. Open `ML_project.ipynb`.
4. Run the notebook cells from top to bottom.
5. The analysis and visualizations will be generated.
6. Forecast outputs will be written to the `outputs/` directory.

---

## Generated Outputs

The notebook generates:

| File | Purpose |
|---|---|
| `forecast.csv` | 12-month forecast with lower and upper ranges |
| `forecast.png` | Historical sales and future forecast |
| `actual_vs_pred.png` | Actual vs predicted sales during testing |
| `error_by_month.png` | Monthly forecasting errors |

---

## Limitations

The forecast has several limitations:

- The dataset contains only a few years of historical observations.
- Promotions are not explicitly modeled.
- Holidays are not explicitly modeled.
- Pricing changes are not explicitly modeled.
- Future business conditions may differ from historical conditions.
- The reported MAPE of approximately 21.7% indicates that predictions still contain meaningful uncertainty.

Therefore, the forecast should be used as a **planning aid**, not as a guaranteed sales target.

---

## Future Improvements

Possible improvements include:

- Add holiday and festival features.
- Include promotional campaign data.
- Include product-level forecasting.
- Include regional forecasting.
- Add pricing information.
- Compare additional time-series models such as ARIMA/SARIMA.
- Test advanced ML models such as Random Forest, XGBoost, or Gradient Boosting.
- Use rolling/expanding time-series cross-validation.
- Build an interactive Power BI or Streamlit dashboard.
- Automate forecast generation when new sales data is uploaded.

---

## Key Takeaway

This project demonstrates how historical retail sales data can be transformed into a practical forecasting workflow.

The final implementation compares multiple forecasting methods and selects **Linear Regression** based on the lowest RMSE. The resulting forecast estimates approximately **$795,694 in sales over the next 12 months**, representing an **8.5% increase** compared with the previous 12-month period in the notebook's analysis.

The forecast can support inventory, staffing, cash-flow, marketing, and business planning decisions.

---

## Author

**Deepak Kumar**

BCA — Artificial Intelligence & Machine Learning

---

## Disclaimer

This project is developed for educational and portfolio purposes. Forecast results depend on the historical dataset and modeling assumptions used in the notebook.
