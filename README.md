# 🚗 Malaysian Used Car Price Prediction Engine

This project provides a data-driven valuation tool for the Malaysian secondary automotive market, aiming to bring transparency to pricing using Machine Learning.

## 🔗 Quick Links
* **Web Page:** [Web Page](https://chee613.github.io/DS-Assignment/)
* **Google Colab Notebook:** [View Notebook](https://colab.research.google.com/drive/1gnwZ9FL3ajXFt7g8i3ikKL2sMaucscfq?usp=sharing)
* **Data Dictionary (Table 1 & 2):** [View Data Statistics](https://colab.research.google.com/drive/1S83DeIjWubVneDvFnLbWUuyN4vijC194?usp=sharing)

## 📄 1. Executive Summary ✨
This project developed a pricing engine for the Malaysian used car market with **88.26% accuracy** (R-Squared). By analyzing a dataset of 4,000 active listings, the final model successfully reduced prediction error by over **RM 10,784** per vehicle compared to baseline linear models. The engine accounts for brand prestige, manufacturing origin, and technical specifications to provide fair market value estimates. 🎯

## 🔍 2. Problem Statement ❓
The used car market in Malaysia is often characterized by information asymmetry. This project addresses three primary uncertainties:
* **Engine Displacement:** Does a larger engine justify a higher price, or is it just a luxury proxy? 📏
* **Geographic Dynamics:** Does purchasing a vehicle in a different state (e.g., Perak vs. KL) offer significant savings? 📍
* **Brand Origin:** Is Continental luxury prestige offset by steeper depreciation compared to Asian brands? 🌎

## 📊 3. Data Overview 🗂️
The analysis utilized 4,000 active car listings from <mark>**carlist_scraped_data.csv**</mark>. Key data points extracted include:
* **📝 Description:** Raw text used to derive Year, Brand, Origin and Engine Capacity (L).
* **💰 List_Price:** The target variable (Mean: RM 82,074).
* **🛣️ Mileage:** Average distance driven (Mean: ~95,187 KM).
* **🚘 Model:** Specific car names (e.g., Perodua Myvi, Honda City).
* **🗺️ Location:** Seller's region, processed into State (e.g., Selangor, Kuala Lumpur).
* **⚙️ Gear_Type:** Predominantly Automatic (97.8%).

## 🛠️ 4. Methodology & Workflow ⚙️
The project followed a structured data science pipeline:
1.  **🧹 Data Preprocessing:** currency parsing, mileage ranges to averages, Car_Age calculation (2025 baseline), data extraction from description(year, brand, origin) and location generalisation
2.  **📈 Target Transformation:** Applied **Log-Transformation** to `List_Price` to handle high right-skewness from luxury supercars.
3.  **🔎 EDA:** Performed bivariate and multivariate regression to validate market hypotheses.
4.  **🤖 Modeling:** Compared a **Linear Regression** baseline against a tuned **Random Forest Regressor**.

## 🏆 5. Model Results ✅
The **Random Forest Regressor** was the winner, capturing complex non-linear interactions.

| Model | R2 Score (Accuracy) | RMSE (Avg. Error) | Verdict |
| :--- | :--- | :--- | :--- |
| Linear Regression | 67.54% | RM 55,123 | Underfitting ❌ |
| **Random Forest** | **88.26%** | **RM 44,339** | **Winner 🏆** |

## 💡 6. Key Insights 🧠
* **🚀 Primary Driver:** **Engine Size** is the most critical factor (32.6% importance), setting the "price ceiling."
* **🗓️ Age vs. Usage:** **Car Age** (25.8%) is nearly twice as influential as **Mileage** (12.8%). Malaysians prioritize the model year!
* **🏙️ The Urban Premium:** Identical models in Kuala Lumpur maintain higher prices than those in Perak, reflecting high urban demand.
* **📉 Depreciation:** Continental brands exhibit a significantly steeper depreciation curve compared to Asian brands.

## 💻 7. How to Use the Model 🚀

You can use the trained model files to predict resale prices for new listings.

### Dependencies

```python
import pandas as pd
import numpy as np
import joblib
The model can be used to predict prices via the `predict_car_price` function:
```
### Prediction Code Snippet
### Load Model and Feature Map
```python
model = joblib.load('my_car_price_model.pkl')
model_columns = joblib.load('model_columns.pkl')

# Example Input (Note: Data must be preprocessed to match training columns)
prediction_log = model.predict(input_data)
price_rm = np.expm1(prediction_log) # Convert log back to RM

print(f"Recommended Resale Price: RM {price_rm}")
```

### OR
```python
# Example: Estimating a 2018 Honda Civic price
prediction = predict_car_price(
    year=2018,
    mileage=60000,
    engine_l=1.8,
    brand='Honda',
    origin='Asian',
    state='Selangor',
    is_warranty=False
)

print(f"💰 Estimated Price: RM {prediction:,.2f}")
```
