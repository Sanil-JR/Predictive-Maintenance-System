# ✈️ Predictive Maintenance — RUL Estimation (NASA CMAPSS)

Predicting the **Remaining Useful Life (RUL)** of aircraft jet engines using sensor time-series data from the NASA CMAPSS dataset.

---

## 📌 Problem Statement

Aircraft engines generate continuous sensor data during operation. As components degrade over time, failure risk increases. Unplanned failures cause:

* 🔴 **Safety risks** — catastrophic failure mid-flight
* 💰 **High costs** — emergency maintenance is 3–5x more expensive than scheduled
* ⏱️ **Downtime losses** — airlines lose ~$150K/hour per grounded aircraft

**Goal:** Predict how many operational cycles remain before an engine fails — enabling maintenance *before* failure, not *after*.

> **RUL** = Number of operational cycles remaining before engine failure

---

## 📂 Dataset

**NASA CMAPSS** (Commercial Modular Aero-Propulsion System Simulation)

| Dataset | Engines | Operating Conditions | Fault Modes | Difficulty |
| ------- | ------- | -------------------- | ----------- | ---------- |
| FD001   | 100     | 1                    | 1           | Easy       |
| FD002   | 260     | 6                    | 1           | Medium     |
| FD003   | 100     | 1                    | 2           | Medium     |
| FD004   | 249     | 6                    | 2           | Hard       |

**26 columns per file:** `engine_id`, `cycle`, `operational_setting_1/2/3`, `sensor_1` to `sensor_21`

📥 Download: https://www.nasa.gov/content/prognostics-center-of-excellence-data-set-repository

---

## 🗂️ Project Structure

```text
predictive-maintenance-rul/
│
├── notebooks/
│   └── predictive_maintenance_full.ipynb
│
├── data/
│   ├── train_FD001.txt
│   ├── train_FD002.txt
│   ├── train_FD003.txt
│   └── train_FD004.txt
│
├── models/
│
├── README.md
└── requirements.txt
```

---

## 🔄 Pipeline

Each of the 4 datasets goes through the same pipeline independently:

```text
Load Dataset
    ↓
Create RUL (clipped at 125 cycles)
    ↓
EDA
    ↓
Feature Selection
    ↓
Rolling Mean Features
    ↓
Train/Test Split
    ↓
MinMax Scaling
    ↓
Random Forest + XGBoost
    ↓
Model Comparison
```

Then cross-dataset results are combined into a unified comparison table.

---

## ⚙️ Key Design Decisions

### 1. RUL Clipping at 125

Raw RUL goes 300+ cycles for new engines. Model wastes capacity learning the perfectly healthy phase. Clipping at 125 focuses training on the degradation phase that actually matters.

### 2. Engine-wise Train/Test Split

Random row splitting causes data leakage. Instead, whole engines are assigned to train or test sets.

### 3. Dynamic Feature Detection

FD001/FD003 have one operating condition, so operational settings are constant and removed.

FD002/FD004 have multiple operating conditions, so settings are retained.

### 4. Rolling Mean Features

Rolling mean over 10 cycles per engine captures degradation trends and reduces sensor noise.

---

## 📊 Results

| Dataset | Model         | MAE   | RMSE  | R²     |
| ------- | ------------- | ----- | ----- | ------ |
| FD001   | Random Forest | ~10.2 | ~15.4 | ~0.863 |
| FD001   | XGBoost       | ~10.3 | ~15.6 | ~0.861 |
| FD002   | Random Forest | ~12.4 | ~17.5 | ~0.825 |
| FD002   | XGBoost       | ~11.8 | ~16.7 | ~0.841 |
| FD003   | Random Forest | ~8.7  | ~13.7 | ~0.888 |
| FD003   | XGBoost       | ~8.6  | ~13.1 | ~0.897 |
| FD004   | Random Forest | ~13.7 | ~20.2 | ~0.756 |
| FD004   | XGBoost       | ~13.3 | ~19.6 | ~0.769 |

> **XGBoost outperforms Random Forest across all four datasets.**

**Best Overall Model:** FD003 XGBoost
RMSE = 13.14
R² = 0.897

---

## 💼 Business Impact

An RMSE of approximately 18 cycles means predictions are accurate within about 18 flight cycles.

This provides roughly an **18-day early warning window** for maintenance planning.

### Engine Risk Classification

| Zone        | RUL Threshold | Action               |
| ----------- | ------------- | -------------------- |
| 🔴 Critical | < 30 cycles   | Immediate inspection |
| 🟠 Warning  | 30–60 cycles  | Schedule maintenance |
| 🟢 Safe     | > 60 cycles   | Continue monitoring  |

**Estimated Savings:** ~$400K per avoided emergency maintenance event.

---

## 🔍 Explainability

SHAP (SHapley Additive exPlanations) is used to explain XGBoost predictions and identify which sensors contribute most to Remaining Useful Life estimation.

---

## 🚀 How to Run

### Clone Repository

```bash
git clone https://github.com/your-username/predictive-maintenance-rul.git
cd predictive-maintenance-rul
```

### Install Requirements

```bash
pip install -r requirements.txt
```

### Run Notebook

```bash
jupyter notebook predictive_maintenance_full.ipynb
```

Run all cells from top to bottom.

---

## 📦 Requirements

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
shap
joblib
jupyter
```

---

## 🔮 Future Improvements

| Improvement           | Benefit                           |
| --------------------- | --------------------------------- |
| LSTM / GRU            | Better temporal sequence learning |
| Hyperparameter Tuning | Improved predictive performance   |
| Real Turbofan Data    | Better real-world validation      |

---

## 📁 Saved Models

```text
rf_FD001.pkl
xgb_FD001.pkl
scaler_FD001.pkl

rf_FD002.pkl
xgb_FD002.pkl
scaler_FD002.pkl

rf_FD003.pkl
xgb_FD003.pkl
scaler_FD003.pkl

rf_FD004.pkl
xgb_FD004.pkl
scaler_FD004.pkl
```

---

## 🛠️ Skills Demonstrated

* Predictive Maintenance
* Machine Learning
* Feature Engineering
* Time Series Analysis
* Random Forest
* XGBoost
* SHAP Explainability
* Python
* Pandas
* Scikit-learn

---

## 👤 Author

**Sanil J R**

Mechanical Engineer | Data Science Enthusiast

---

## 📄 License

This project uses the NASA CMAPSS dataset for educational and research purposes.
