# Ripple-Effects-Tariffs-Trade-Disruptions-in-Global-Commerce
### *A Big Data Analytics & Machine Learning Project Using Apache Spark*

---

## **📌 Project Overview**

Global trade has undergone significant volatility over the last two decades due to tariff reforms, geopolitical tensions, supply-chain shocks, and shifting economic alliances.
This project investigates the *real “ripple effects”* of tariff fluctuations on global trade by integrating:

* **Million-row bilateral trade datasets (UN Comtrade / WITS)**
* **Tariff schedules from WTO / WITS Tariff**
* **Apache Spark–based distributed ETL & analytics**
* **Sector-level research questions**
* **A Spark ML forecasting model**

Our goal is to determine *where* tariff changes significantly influence trade, *how* disruptions propagate across partners and sectors, and *whether* machine learning models can predict trade flows using tariff and historical patterns.

---

## **📂 Repository Structure**

---

## **🛠️ Technologies Used**

### **Big Data & Distributed Systems**

* **Apache Spark (PySpark)**

  * Distributed ETL
  * Window functions
  * Joins & aggregations
  * Spark MLlib pipeline training

### **Storage & File Formats**

* **Parquet** (columnar, compressed, efficient for Spark)
* CSV for raw input files
* Git/GitHub for version control & collaboration

### **Visualization**
* Matplotlib/Seaborn inside PySpark notebooks

---

## **📑 Data Sources**

### **Trade Data**

* Source: *World Integrated Trade Solution (WITS) / UN Comtrade*
* Granularity: **HS-4**, 2007–2025
* Columns:

  * Reporter, Partner, Year
  * ProductCode
  * TradeValue (in 1000 USD)

### **Tariff Data**

* Source: *WTO Tariff / WITS Tariff Database*
* Years: **2007–2022**
* Columns:

  * Simple Average Duty
  * Weighted Average Duty
  * Min/Max tariffs
  * Binding coverage
  * Product-level tariff lines

Trade and tariff datasets were merged on:
**Reporter × Partner × ProductCode × Year**

---

## **🔧 Spark ETL Workflow**

The complete distributed ETL workflow includes:

1. **Importing multi-million row CSV files** into Spark
2. **Cleaning & standardizing country names (Reporter/Partner)**
3. **Casting numerical fields** (`Year`, `TradeValueKUSD`, duty rates)
4. **Dealing with missing years & missing tariff rows**
5. **Mapping HS-4 to sectors** (Electronics, Vehicles, Chemicals, etc.)
6. **Merging trade + tariff datasets**
7. **Saving final dataset as Parquet** for efficient downstream modeling

All ETL operations were executed through the Spark distributed engine to handle the large file sizes.

---

## **🔍 Research Questions (RQ)**

### **RQ1 — How do tariff fluctuations influence trade values across major sectors?**

---

### **RQ2 — How can we quantify and predict the short-term sensitivity of international product-country level trade flows to tariff shocks?**


---

### **RQ3 - Which countries tend to shift their trade partners (diversion effect) when tariffs rise on certain goods?**

---

## **🤖 Machine Learning Model: Spark ML Pipeline**

We trained a **Gradient-Boosted Trees Regressor (GBT)** using Apache Spark MLlib to forecast trade values.

### **ML Objective**

Predict annual **TradeValueKUSD** using:

* Historical lag (`lag1_trade`)
* Tariff features (`SimpleAvgDuty`, `WeightedAvgDuty`)
* Sector
* Reporter–Partner pair
* Year

### **Pipeline Steps**

1. **Feature Engineering**

   * Lag features
   * Sector encoding
   * StringIndexer + OneHotEncoder for reporter/partner names
2. **VectorAssembler**
3. **Train–test split (time-based)**
4. **Baseline model:**

   * Prediction = last year's trade
5. **GBT Model Training**
6. **Evaluation:** RMSE and R²
7. **Comparison with baseline**

### **Summary of Results**

| Model                   | RMSE         | R²          | Interpretation                                           |
| ----------------------- | ------------ | ----------- | -------------------------------------------------------- |
| **Baseline (lag-only)** | Moderate     | ~0.60       | History explains trade well                              |
| **GBT Regressor**       | *Lower RMSE* | *Higher R²* | Tariffs + sector + partner info improve predictive power |

📌 **Key Insight:**
Trade is highly persistent year-to-year (lag feature strongest). Tariffs add incremental predictive power but do not overhaul predictions. The ML results confirm our analytical findings.

---

## **🏁 Conclusion**

This project combines large-scale data engineering, economic analysis, and machine learning to study tariff-driven trade disruptions.

**What we achieved:**

* Built an end-to-end **Spark ETL pipeline** processing millions of rows
* Merged complex international datasets (trade + tariff)
* Investigated global trade behavior using sector-level analysis
* Trained a predictive ML model entirely inside Spark
* Produced dashboards showing real-world trade ripple effects

**Overall Finding:**
Tariffs influence trade, but **global macroeconomic conditions create much larger disruptions**. Tariffs act as amplifiers—not primary drivers.

---

## **👥 Team Members**

* Shruti Karmarkar
* Hrishik Desai
* Aviraj Dongare

---

