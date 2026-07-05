# Hotel ADR Prediction Model using Statistical Feature Engineering

Predicting **Average Daily Rate (ADR)** is a fundamental problem in hotel revenue management. This project develops an interpretable **Ordinary Least Squares (OLS) Regression** model that predicts ADR using carefully engineered features instead of complex black-box algorithms. By combining statistical feature engineering, ranked categorical encodings, and interaction terms, the model explains approximately **70% of the variation** in hotel room prices while remaining easy to interpret.

---

# Overview

This project focuses on building a refined regression model for hotel pricing using a subset of **17 high-impact features** selected from a larger feature pool.

The objective was to:

* Predict hotel Average Daily Rate (ADR)
* Improve interpretability over complex ML models
* Reduce multicollinearity
* Engineer meaningful interaction features
* Extract business insights from statistical significance

---

# Dataset

The project uses the **Hotel Booking Demand Dataset**, containing booking information for both City Hotels and Resort Hotels.

The dataset includes information such as:

* Booking lead time
* Arrival date
* Hotel type
* Market segment
* Meal plan
* Room type
* Number of adults and children
* Booking agent
* Average Daily Rate (Target Variable)

---

# Problem Statement

Predict the **Average Daily Rate (ADR)** using historical booking information while maintaining high interpretability through statistical modeling.

---

# Feature Engineering

The final model consists of **17 engineered features** divided into three groups.

## 1. Standardized Numerical Features

These variables were standardized using Z-score normalization.

| Feature              |
| -------------------- |
| Lead Time            |
| Arrival Year         |
| Arrival Week Number  |
| Arrival Day of Month |
| Adults               |
| Children             |

---

## 2. Encoded Categorical Features

Instead of one-hot encoding, categorical variables were transformed using ranked historical pricing information.

| Feature            | Encoding                     |
| ------------------ | ---------------------------- |
| Hotel Type         | Binary Encoding              |
| Arrival Month      | Ranked Label Encoding        |
| Meal Plan          | Ranked by ADR Premium        |
| Market Segment     | Ranked by Historical Premium |
| Reserved Room Type | Ordered Integer Mapping      |
| Agent Available    | Binary                       |
| Top Agent          | Binary                       |

---

## 3. Engineered Interaction Features

To capture non-linear relationships, several interaction terms were created.

### Season × Hotel Interaction

Captures seasonal differences between Resort and City Hotels.

Formula:

```text
Arrival_Month_Rank × (Hotel + 1)
```

---

### Lead Time × Stay Duration

Captures booking behavior differences.

Formula:

```text
ln(Lead_Time + 1) × Total_Stay_Nights
```

---

### Polynomial Seasonality

The month ranking was expanded using polynomial terms.

```text
Month²
Month³
```

---

### Solo Traveler Indicator

```text
1 if Adults = 1 and Children = 0
Else 0
```

---

# Model

Algorithm:

* Ordinary Least Squares (OLS) Regression

Why OLS?

* Highly interpretable
* Easy coefficient analysis
* Statistical significance testing
* Explainable business decisions

---

# Model Performance

| Metric   |      Value |
| -------- | ---------: |
| R² Score | **0.7028** |
| RMSE     |  **26.12** |
| MAE      |  **19.08** |

The refined model explains approximately **70% of ADR variation** while using only **17 carefully selected features**.

---

# Business Insights

## 1. Seasonality Drives Pricing

The interaction between hotel type and season is the strongest predictor.

**Business Impact**

* Resort hotels command significantly higher seasonal premiums.
* Pricing strategies should differ between Resort and City Hotels.

---

## 2. Room Type Matters

Reserved room category strongly influences ADR.

**Business Impact**

* Upselling premium room categories at booking is more valuable than post-booking upgrades.

---

## 3. Direct Bookings Generate Higher ADR

Market segment and booking source significantly affect pricing.

**Business Impact**

* Investing in direct booking channels can increase ADR while reducing commission costs.

---

## 4. Booking Window Effects

Lead time interacts with stay duration.

**Business Impact**

* Long-lead long-stay bookings deserve different pricing than last-minute reservations.

---

## 5. Remaining Variance

Approximately **30%** of ADR variation remains unexplained.

Possible factors include:

* Local events
* Competitor pricing
* Holidays
* Weather
* Demand fluctuations
* Dynamic pricing decisions

---

# Project Structure

```text
Hotel-ADR-Prediction/
│
├── data/
│   ├── hotel_bookings.csv
│
├── notebooks/
│   ├── Exploratory_Data_Analysis.ipynb
│   ├── Feature_Engineering.ipynb
│   ├── Model_Training.ipynb
│
├── models/
│   ├── final_ols_model.pkl
│
├── images/
│   ├── correlation_heatmap.png
│   ├── feature_importance.png
│   ├── residual_plot.png
│
├── requirements.txt
├── README.md
└── LICENSE
```

---

# Technologies Used

* Python
* Pandas
* NumPy
* Statsmodels
* Scikit-learn
* Matplotlib
* Seaborn
* Jupyter Notebook

---

# Future Improvements

* Incorporate local event calendars
* Add competitor pricing data
* Include weather information
* Compare OLS with XGBoost and LightGBM
* Deploy as a REST API
* Build an interactive pricing dashboard

---

# Results

The project demonstrates that **careful statistical feature engineering can achieve strong predictive performance without sacrificing interpretability**.

Rather than relying solely on complex machine learning algorithms, this model provides actionable business insights into the factors that influence hotel pricing while maintaining a robust predictive accuracy (**R² = 0.7028**).

---

# Author

**Aman**

Data Analytics | Machine Learning | Revenue Analytics | Statistical Modeling
