
# AI/ML Internship - Task 2: Short-Term Stock Price Prediction Using Linear Regression

## 📌 Task Objective
The objective of this project is to model financial time-series trends by building a predictive engine that forecasts the **next day's closing price** of a specific stock using historical transaction signatures. Rather than estimating contemporary outputs from parallel variables (which yields minimal future value), this project introduces an engineered lagging framework—utilizing today's `Open`, `High`, `Low`, and `Volume` profiles to project tomorrow's asset valuations.

---

## 📊 Dataset Profiles
Live historical financial records are extracted programmatically using the **`yfinance` API** framework.
* **Ticker Profile**: Apple Inc. (`AAPL`)
* **Temporal Windows**: 2 Years of continuous daily trading data
* **Features Analysed**: `Open`, `High`, `Low`, `Close`, `Volume`
* **Target Feature**: `Next_Close` (Engineered via a `-1` row operational temporal translation shift)

---

## 🛠️ Step-by-Step Implementation Pipeline

### 1. Environment Configuration & Package Installation
Deploys core runtime components necessary for programmatic data extraction, transformation, visualization, and predictive modeling:
* `yfinance` for live data streaming from market endpoints.
* `pandas` & `numpy` for matrix layout mutations and vector operations.
* `scikit-learn` for regression engine orchestration.
* `matplotlib` & `seaborn` for generating timeline graphs.

### 2. Feature Engineering & Shifting Core Operations
* Downloads clean tabular matrices and executes defensive validation checks to clean potential multi-index headers.
* Introduces a target lagging strategy by shifting the historical `Close` series up by one step (`shift(-1)`) to establish a true future prediction window.
* Sanitizes structural artifacts by removing the final index row containing null reference points (`.dropna()`).

### 3. Chronological Time-Series Partitioning
* **Strict Non-Shuffled Splitting**: To prevent temporal data leakage, data rows are divided sequentially (80% Training / 20% Testing) without structural randomization. This preserves the authentic timeline continuity of market patterns.

### 4. Regression Architecture & Metric Validation
* Instantiates and trains an Ordinary Least Squares (OLS) **Linear Regression Model**.
* Scores prediction accuracy across standard statistical indices including Mean Absolute Error (MAE), Mean Squared Error (MSE), and the Coefficient of Determination ($R^2$ Score).

---

## 🏆 Key Results & Analytical Findings

### 📈 Data & Visualization Insights
* **Correlation Dominance**: Linear correlation maps show that today's price dimensions (`Close`, `High`, `Low`, `Open`) maintain an exceptionally strong linear relationship with tomorrow's price target. Transaction metrics (`Volume`) demonstrate a significantly weaker direct linear link to future price changes.
* **Trend Alignment**: Scatter plots and overlay charts show the model closely tracks macroeconomic market trends and direction switches over long time frames.

### ⚠️ Performance Profile & The "Lag" Phenomenon
* **The "Lag" Catch**: Detailed inspection of the actual vs. predicted price plots reveals a classic time-series artifact: the predicted price line acts as a slight shadow, lagging behind actual market movements by roughly one day.
* **Algorithmic Explanation**: This occurs because an OLS Linear Regression engine heavily weights the most recent known `Close` vector when projecting future steps.
* **Strategic Verdict**: While Linear Regression serves as a strong baseline model for establishing overall trend directions, capturing sudden spikes, gap downs, or news-driven volatility requires moving to sequential frameworks like Long Short-Term Memory (LSTM) neural networks or GARCH error modeling architectures.

---
