
# AI/ML Internship - Task 6: House Price Prediction Using Regression Analysis

## 📌 Task Objective
The objective of this project is to build a predictive machine learning regression engine capable of forecasting real estate market valuations based on physical asset features and spatial variables. This project demonstrates essential data engineering skills, including feature scaling, categorical variable encoding, and regression error evaluation.

---

## 📊 Dataset Profiles & Engineered Features
The dataset consists of residential property records mapped across several structural properties:
* **Predictor Features (X):**
  * `Square Footage` (Continuous Numerical - core linear driver)
  * `Bedrooms / Bathrooms` (Discrete Numerical features)
  * `Neighborhood / Location` (Categorical variable encoded for structural proximity analysis)
* **Target Feature (Y):** `Price` (Continuous Numerical target valuation)

---

## 🛠️ Data Pipeline & Architecture

### 1. Preprocessing & Feature Scaling
* **Mathematical Weight Alignment:** Because physical variables use drastically different numerical spaces (e.g., square footage scales in the thousands, while bedroom counts scale under ten), the pipeline applies `StandardScaler`. This centers all continuous features to a mean of 0 and a standard deviation of 1, preventing distance calculation biases.
* **Categorical Location Mapping:** Spatial coordinates and neighborhood identities are handled appropriately to allow the regression engine to process geographic premium shifts.

### 2. Validation & Performance Framework
* **Data Splits:** The matrix is split using an 80/20 train-test validation boundary to ensure reliable out-of-sample performance tracking.
* **Error Metrology:** The model is graded using complementary regression metrics:
  * **Mean Absolute Error (MAE):** Tracks the average absolute distance of error margins.
  * **Root Mean Squared Error (RMSE):** Penalizes larger error deviations more heavily, highlighting variance driven by luxury outliers.

---

## 🏆 Key Results & Analytical Findings

### 📈 Data & Visualization Insights
* **The Dominance of Scale:** Exploratory plots confirm that total square footage remains the single strongest linear indicator of a property's market price.
* **The Location Premium:** Adding neighborhood tracking significantly reduced prediction error variances in localized premium zones, capturing market trends that raw property dimensions alone could not explain.

### 📉 Model Evaluation & Performance Profiles
* **Diagonal Structural Alignment:** The **Actual vs. Predicted Price** scatter plot displays a tight diagonal path, indicating that the baseline regression model successfully captures primary valuation patterns.
* **The Outlier Penalty:** The calculated **RMSE** is notably higher than the **MAE**. Mathematically, this confirms the presence of high-value luxury home outliers, where the model's standard linear predictions underperformed relative to normal residential tiers.
* **Future Optimization Roadmap:** To handle this structural skewness in future iterations, the target vector should undergo a logarithmic transformation (`log1p`) to compress high-value luxury deviations and improve overall prediction consistency.

---
