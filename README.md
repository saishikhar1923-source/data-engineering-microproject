# 📊 Interactive Business Intelligence Dashboard with Machine Learning

A Power BI dashboard that uses Machine Learning to predict customer churn and display business insights through interactive visualizations.

---

## 🧠 What Does This Project Do?

This project:
1. **Generates** a realistic dataset of 1000 customers using Python
2. **Trains** a Machine Learning model to predict which customers might leave (churn)
3. **Exports** the predictions to CSV files
4. **Visualizes** everything in an interactive Power BI dashboard with KPIs, charts, and filters

---

## 📁 Project Structure

```
bi_dashboard/
│
├── ml_pipeline.py          # Generates data + trains ML model + exports CSVs
├── load_to_sql.py          # (Optional) Load CSVs into SQL Server
│
└── output/                 # All CSV files go here after running ml_pipeline.py
    ├── customer_predictions.csv
    ├── model_metrics.csv
    ├── confusion_matrix.csv
    ├── monthly_trends.csv
    └── feature_importance.csv
```

---

## 🛠️ Tools & Technologies Used

| Tool | Purpose |
|---|---|
| Python 3 | Data generation and ML model |
| Pandas | Data manipulation |
| NumPy | Numerical operations |
| Scikit-learn | Machine Learning (Random Forest) |
| CSV files | Data storage and transfer |
| Power BI Desktop | Dashboard and visualizations |
| DAX | Business KPI calculations |

---

## ⚙️ How to Run This Project

### Step 1: Install Python
Download Python from https://www.python.org/downloads/ and install it.

### Step 2: Install Required Libraries
Open your terminal (or VS Code terminal) and run:

```bash
pip install pandas numpy scikit-learn sqlalchemy
```

### Step 3: Create the Output Folder
Inside your project folder, create a folder called `output`. Or just let the script do it automatically (it's handled in the code).

### Step 4: Run the ML Pipeline
In your terminal, navigate to your project folder and run:

```bash
python ml_pipeline.py
```

You should see this output:
```
✅ All CSV files exported successfully!
Model Accuracy: 100.0%
Churn Rate: 11.7%

Files created:
  • customer_predictions.csv
  • model_metrics.csv
  • confusion_matrix.csv
  • monthly_trends.csv
  • feature_importance.csv
```

### Step 5: Open Power BI Desktop
Download Power BI Desktop for free from https://powerbi.microsoft.com/desktop

### Step 6: Connect Power BI to Your CSV Files
1. Open Power BI Desktop
2. Click **Get Data → Text/CSV**
3. Import each of the 5 CSV files from your `output/` folder one by one
4. Click **Load** for each file

### Step 7: Build the Dashboard
Follow the dashboard setup below to recreate all 4 pages.

---

## 📊 Dashboard Pages

### Page 1 — KPI Overview
Shows the big picture at a glance.
- **Cards:** Total Customers, Churn Rate %, Total Revenue, Model Accuracy
- **Donut chart:** Customer breakdown by Risk Category (Low / Medium / High)
- **Bar chart:** Churn Rate by Region
- **Slicers:** Filter by Year, Region, Product Category

### Page 2 — Prediction Trends
Shows how churn changes over time.
- **Line chart:** Monthly churned customers and churn rate
- **Area chart:** Average churn probability by month
- **Column chart:** Churn rate by Product Category and Risk Category

### Page 3 — Risk Categories
Helps identify which customers are at risk.
- **Stacked bar chart:** Risk category breakdown by Region
- **Table:** Customer list sorted by churn probability (highest risk first)
- **Scatter plot:** Credit Score vs Purchase Amount colored by Risk

### Page 4 — Model Performance
Shows how well the ML model is working.
- **Bar chart:** Accuracy, Precision, Recall, F1 Score
- **Table:** Confusion matrix (True/False Positives and Negatives)
- **Bar chart:** Feature importance (which factors drive churn the most)
- **Cards:** Model Accuracy % and F1 Score

---

## 🤖 Machine Learning Details

**Algorithm:** Random Forest Classifier

**What it predicts:** Whether a customer will churn (leave) or not

**Input features used:**
- Age
- Annual Income
- Purchase Amount
- Number of Transactions
- Credit Score
- Region
- Product Category
- Month

**Output:**
- `Churn_Prediction` — 0 (won't churn) or 1 (will churn)
- `Churn_Probability` — a score from 0.0 to 1.0
- `Risk_Category` — Low Risk / Medium Risk / High Risk

**Model Performance:**

| Metric | Value |
|---|---|
| Accuracy | ~100% |
| Precision | ~100% |
| Recall | ~100% |
| F1 Score | ~0.98 |

> Note: High scores are expected because the dataset is synthetically generated with clear patterns.

---

## 📐 DAX Measures (Power BI Formulas)

These are the custom calculations created in Power BI:

```
Total Customers = COUNTROWS(customer_predictions)

Churned Customers = 
    CALCULATE(
        COUNTROWS(customer_predictions),
        customer_predictions[Churn_Prediction] = 1
    )

Churn Rate % = 
    DIVIDE([Churned Customers], [Total Customers], 0) * 100

Total Revenue = SUM(customer_predictions[Purchase_Amount])

Model Accuracy % = 
    CALCULATE(
        MAX(model_metrics[Value]),
        model_metrics[Metric] = "Accuracy"
    ) * 100
```

---

## 💡 Business Insights This Dashboard Provides

- Which **region** has the highest churn risk
- Which **product category** loses the most customers
- How churn rate **changes month to month**
- Which **individual customers** are high risk (can be targeted for retention campaigns)
- How much **revenue is at risk** from high-risk customers
- How **reliable the ML model** is at predicting churn

---

## 🗂️ CSV File Reference

| File | Key Columns | Used For |
|---|---|---|
| `customer_predictions.csv` | CustomerID, Churn_Prediction, Churn_Probability, Risk_Category | Main prediction data |
| `model_metrics.csv` | Metric, Value, Percentage | Accuracy/F1/Precision cards |
| `confusion_matrix.csv` | Category, Count, Actual_Label, Predicted_Label | Confusion matrix visual |
| `monthly_trends.csv` | Year, Month, Churn_Rate, Avg_Revenue | Line and trend charts |
| `feature_importance.csv` | Feature, Importance | Feature importance bar chart |

---

## ❓ Common Issues & Fixes

**Problem:** `ModuleNotFoundError` when running the Python script  
**Fix:** Run `pip install pandas numpy scikit-learn` in your terminal

**Problem:** CSV files not found in Power BI  
**Fix:** Make sure you ran `ml_pipeline.py` first and check the `output/` folder exists

**Problem:** Power BI shows "Sum of..." instead of actual values  
**Fix:** Click the column in the Values well → select "Don't summarize"

**Problem:** SQL connection error in `load_to_sql.py`  
**Fix:** Skip that file entirely — connect Power BI directly to the CSV files instead

---

## 👨‍💻 Project Info

**Course:** Faculty of Engineering and Technology  
**Institution:** Alliance School of Advanced Computing, Alliance University  
**Purpose:** Academic project demonstrating BI dashboard development with ML integration

--

##Team (8)

# Team Members

| Name | Registration Number |
|---|---|
| Mohammed Ayaan Adil Ahmed | 2411021061286 |
| Ibadul Azam | 2411021060840 |
| N Siva Sruthi | 2411021060566 |
| D Sai Shikhar Achari | 2411021060542 |
