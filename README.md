# 🌍 Global Temperature Change Prediction

📅 **Date:** October 20, 2024

---

## 📘 Introduction

This project aims to **predict yearly temperature changes** for cities across a selected time period using **time series forecasting models** — specifically **ARIMA** and **LSTM**.

It also:
- Identifies the **top 10 Indian cities** projected to experience the most drastic climate changes from 2013–2023.
- Explores the **correlation between pollution levels and temperature change**.
- Predicts **Greenhouse Gas (GHG) emissions** and their effect on global temperatures.

---

## 🎯 Objectives

1. Predict the temperature of a selected city over a chosen time period.
2. Forecast the **top 10 Indian cities** with the greatest expected temperature changes.
3. Analyze the relationship between **GHG emissions** (Methane, CO2, HCFC) and predicted temperatures.
4. Compare **ARIMA and LSTM** model predictions and explore model agreement.

---

## 🧠 Methodology

### 📊 Data Source

We use the **Climate Change: Earth Surface Temperature Data** from [Kaggle](https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data).

### 🧹 Data Preprocessing

- Converted `'dt'` column to `DateTime` format.
- Filtered Indian cities from the global dataset.
- Removed rows with missing or invalid values.
- Grouped by year and calculated average temperature.
- Used log/differencing transformation to make the data stationary (for ARIMA).
- Normalized data for LSTM input.

---

## ⚙️ Model Workflows

### 🔁 ARIMA (AutoRegressive Integrated Moving Average)

**Workflow:**

1. Ensure **stationarity** (required for ARIMA).
2. Use **Augmented Dickey-Fuller (ADF)** test to confirm stationarity.
3. Apply **differencing** if required.
4. Use **Grid Search** to find optimal `(p, d, q)` values.
5. Fit the ARIMA model to the training data.
6. Forecast future temperatures.
7. Evaluate using **Mean Squared Error (MSE)**.

**Key Strengths:** Effective for short-term, linear trends in stationary data.

---

### 🔮 LSTM (Long Short-Term Memory Network)

**Workflow:**

1. Normalize and reshape data into supervised time series format.
2. Split data into training and validation sets.
3. Define an LSTM architecture:
   - Input → LSTM Layer → Dense Layer → Output
4. Train model over multiple epochs with `Adam` optimizer.
5. Forecast future temperatures using test sequences.
6. Evaluate with **MSE**, **RMSE**, and visual comparisons.

**Key Strengths:** Captures **non-linear patterns** and **long-term dependencies**.

---

## 🔍 Correlation Analysis (Heatmap Insights)

This section uses a heatmap to analyze the **correlation between GHG emissions** and the temperature predictions from ARIMA and LSTM.

| GHG Variable      | Temp_ARIMA | Temp_LSTM | Observation |
|------------------|-------------|------------|-------------|
| **Methane_ARIMA** | **0.65**     | -0.60       | Strong positive w/ ARIMA; opposite with LSTM |
| **CO2_ARIMA**     | -0.52        | -0.87       | Both show negative correlation (LSTM stronger) |
| **HCFC_ARIMA**    | **0.71**     | **0.63**     | Strong agreement across both |
| **Methane_LSTM**  | -0.28        | **0.92**     | LSTM shows very strong positive |
| **CO2_LSTM**      | -0.33        | **0.89**     | LSTM shows strong positive correlation |
| **HCFC_LSTM**     | -0.37        | **0.87**     | LSTM identifies HCFC as highly impactful |
| **ARIMA vs LSTM** | **0.097**    |              | Very low agreement between models |

### 🧠 Conclusions:
- LSTM models generally detect **stronger positive effects** of GHGs on temperature than ARIMA.
- **HCFC** shows the most consistent positive correlation across both models.
- Methane and CO2 predictions **differ significantly** between models.
- Low agreement (**0.097**) between ARIMA and LSTM temperature outputs suggests **model fusion or further tuning** may improve accuracy.

---

## ✅ Summary of Work

- 📈 Forecasted temperature changes for cities over time.
- 🌆 Identified **top-10 Indian cities** with the most predicted temperature rise (2013–2023).
- 🔬 Analyzed **pollution and GHG emission data** for climate impact.
- 🤖 Developed and compared **ARIMA vs LSTM** forecasting pipelines.
- 📊 Created visual heatmaps for correlation between GHGs and model outputs.

---

## 📂 Project Structure

GlobalTempPrediction/
├── data/ # Input datasets (temperature, pollution, emissions)
├── notebooks/ # Jupyter Notebooks for EDA, modeling, and evaluation
├── models/ # Saved ARIMA/LSTM models
├── src/ # Python scripts for preprocessing, training, utils
│ ├── preprocessing.py
│ ├── arima_model.py
│ ├── lstm_model.py
│ └── utils.py
├── visualizations/ # Heatmaps, trend plots, results
├── README.md # Project documentation
└── requirements.txt # Dependencies
