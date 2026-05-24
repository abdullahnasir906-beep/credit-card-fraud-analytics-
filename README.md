# 🚀 Credit Card Fraud Analytics Dashboard (Power BI)

## 📌 Project Overview
This repository contains an end-to-end Data Analytics project focused on financial security and transaction monitoring. Using a high-dimensional transaction dataset, I transformed raw data into a clean, executive-ready Power BI dashboard designed to help banking leaders quickly isolate and monitor fraudulent financial activities.

---

## 📐 Data Modeling & Architecture (Star Schema)
This project strictly adheres to the **Star Schema** design principles to ensure high performance, optimized DAX execution, and intuitive filtering path compliance—aligning with Microsoft PL-300 certification best practices.

### 🗂️ Table Schema Breakdown
The model is divided into a centralized Fact Table surrounded by fully normalized Dimension Tables:
1. **`Fact Table` (The Centerpiece):** Stores all quantitative transactional metrics. Contains core numeric attributes such as the `Amount` of each transaction, linked securely to dimension tables via surrogate keys.
2. **`Dim_Class` (Dimension Table):** Handles user-friendly transactional categorization. The `Status` column contains categorical labeling (`Fraud` vs `Normal`) which acts as the primary slicing mechanism across all visuals.
3. **`Dim_Features` (Dimension Table):** Captures the high-dimensional structural variables (`V1` to `V28`) resulting from PCA transformation.

### 🔗 Relationship Design
* **Relationship Type:** `1-to-Many (1:*)` unidirectional relationships.
* **Filter Direction:** Filters flow naturally from the Dimension tables down to the Fact table, preventing performance-draining bi-directional ambiguity and data looping.

---

## 🧮 DAX Calculations & Metrics
To avoid hardcoding and maintain full dynamic interactivity across the executive summary, the following DAX measures were constructed:

### 1. Total Amount
Calculates the absolute combined value of all processed credit card transactions.
```dax
Total Amount = SUM('Fact Table'[Amount])

### 2. Total Fraud Amount
Isolates and computes the financial impact of strictly flagged fraudulent transactions.
```dax
Total Fraud Amount = 
CALCULATE(
    [Total Amount],
    'Dim_Class'[Status] = "Fraud"
)

Normal Amount = 
CALCULATE(
    [Total Amount],
    'Dim_Class'[Status] = "Normal"
)
