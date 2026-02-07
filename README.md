# ☀️ Solar Power Generation: Prediction & Fault Detection

### A Data Science approach to forecasting solar output and identifying hardware failures using Linear Regression.

---

## 📖 Overview
This project implements a robust machine learning pipeline to predict the **DC Power Output** of a solar inverter based on environmental sensor data (Irradiation, Ambient Temperature, and Module Temperature).

Beyond simple prediction, this project demonstrates **advanced diagnostic analysis**. By examining model residuals, we identified "broken inverter" anomalies—periods where sunlight was high but power generation was zero—allowing us to quantify the **financial impact of hardware downtime**.

## 🚀 Key Features
* **Physics-Informed Modeling:** Incorporates **Interaction Terms** ($\text{Irradiation} \times \text{Temperature}$) to model the non-linear thermal efficiency loss of solar panels.
* **Diagnostic Refinement:** Uses residual analysis to detect and filter **Heteroscedasticity** and sensor faults.
* **Operational Impact Analysis:** Quantifies lost energy (kWh) and financial loss ($) due to identified inverter failures.
* **Statistical Rigor:** Validated using **5-Fold Cross-Validation** to ensure model stability ($\sigma < 1\%$).

---

## 📊 Dataset
The data is sourced from a solar power plant in India over a 34-day period (Source: [Kaggle](https://www.kaggle.com/datasets/anikannal/solar-power-generation-data)).
* **Granularity:** 15-minute intervals.
* **Volume:** ~68,000 raw rows (Filtered to <10,000 for this analysis).
* **Key Variables:** `DATE_TIME`, `DC_POWER`, `IRRADIATION`, `MODULE_TEMPERATURE`.

---

## 🛠️ Methodology & Pipeline

1.  **Data Cleaning:** Handling 15-minute timestamps and merging generation data with weather sensor readings.
2.  **Exploratory Data Analysis (EDA):** Visualizing the linear correlation between Irradiance and Power, and identifying "Zero Power" outliers.
3.  **Baseline Modeling:** Training a standard Ordinary Least Squares (OLS) Linear Regression model.
4.  **Diagnostic Analysis:**
    * Checked assumptions: **Normality of Residuals** and **Homoscedasticity**.
    * Identified a "Fan Shape" in residuals, indicating efficiency variance at high temperatures.
5.  **Refinement:**
    * Removed "Inverter Fault" anomalies (High Sun / Zero Power).
    * Added **Interaction Features** to capture thermodynamic efficiency limits.
6.  **Business Evaluation:** Calculated total energy lost during fault periods.

---

## 📈 Results

### Model Performance Improvement
We improved the model significantly by moving from a raw baseline to a physics-aware refined model.

| Metric | Baseline Model | Refined Model (Final) | Improvement |
| :--- | :--- | :--- | :--- |
| **RMSE** | 916.26 kW | **508.69 kW** | **~44% Reduction** |
| **R² Score** | 0.9377 | **0.9824** | **+4.5% Accuracy** |
| **Cross-Validation** | N/A | 0.976 (±0.71%) | Highly Stable |

### 💰 Business Impact (Anomaly Detection)
By analyzing the residuals of the baseline model, we identified specific instances of **Inverter Downtime**:
* **Detected Fault Events:** 19 (15-minute intervals)
* **Total Energy Lost:** ~42,657 kWh
* **Estimated Financial Loss:** **~$4,265** (assuming $0.10/kWh)

> *Key Insight: The model serves a dual purpose—forecasting output for grid planning AND acting as an automated alert system for maintenance teams.*

---

## 💻 Dependencies
To run this notebook, you will need the following Python libraries:
* `pandas`
* `numpy`
* `matplotlib`
* `seaborn`
* `scikit-learn`

Install them via pip:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
