# Predictive Maintenance using NASA CMAPSS Dataset

## Project Overview

This project predicts the Remaining Useful Life (RUL) of aircraft engines using NASA's CMAPSS turbofan engine degradation simulation dataset.

The objective is to analyze engine sensor data and build machine learning models that can estimate how many operational cycles remain before engine failure.

---

## Dataset Information

Dataset: NASA CMAPSS FD001

Source: NASA Prognostics Center of Excellence

Dataset Characteristics:

- 100 simulated turbofan engines
- 20,631 records
- 21 sensor measurements
- Multiple operational cycles
- Failure simulation data

Target Variable:

- Remaining Useful Life (RUL)

---

## Objective

To predict the number of operational cycles remaining before engine failure and support predictive maintenance decisions.

---

## Tools Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- XGBoost
- Google Colab
- GitHub

---

## Project Workflow

1. Load NASA CMAPSS FD001 Dataset
2. Create Remaining Useful Life (RUL) Target Variable
3. Perform Exploratory Data Analysis (EDA)
4. Identify Missing Values
5. Detect Constant Sensors
6. Correlation Analysis
7. Feature Selection
8. Data Normalization
9. Train-Test Split
10. Machine Learning Model Training
11. Model Evaluation
12. RUL Prediction

---

## Exploratory Data Analysis (EDA)

Completed Analysis:

- Missing Value Analysis
- Variance Analysis
- Constant Sensor Detection
- Correlation Analysis
- Univariate Analysis
- Bivariate Analysis
- Multivariate Analysis

Important Sensors Identified:

- Sensor 2
- Sensor 3
- Sensor 4
- Sensor 7
- Sensor 8
- Sensor 11
- Sensor 12
- Sensor 13
- Sensor 15
- Sensor 17
- Sensor 20
- Sensor 21

---

## Data Preprocessing

Completed Tasks:

- Removed Constant Sensors
- Selected Important Features
- Applied MinMax Scaling
- Created Training Dataset
- Created Testing Dataset

---

## Project Structure

Predictive-Maintenance-System/

├── app/

├── data/
│   ├── raw/
│   │   └── train_FD001.txt
│   │
│   └── processed/

├── models/

├── notebooks/
│   └── Predictive_Maintenance.ipynb

├── src/

├── README.md

└── requirements.txt

---

## Current Status

Completed:

- Dataset Loading
- RUL Creation
- Exploratory Data Analysis
- Feature Selection
- Data Preprocessing

In Progress:

- Machine Learning Model Training

Upcoming:

- Random Forest Model
- XGBoost Model
- Model Evaluation
- Dashboard Development

---

## Results

Results will be updated after model training and evaluation.

---

## Author

Sanil J R

Data Scientist | Machine Learning

GitHub:
https://github.com/Sanil-JR
