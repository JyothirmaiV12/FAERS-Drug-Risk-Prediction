# **Drug Reaction Analysis Using FAERS Data**

## **Overview**

This project focuses on analyzing adverse drug reactions (ADRs) associated with two drugs commonly used in breast cancer treatment — **Tamoxifen** and **Letrozole**. The data was collected from the **FAERS (FDA Adverse Event Reporting System)** dashboard, processed, and analyzed to identify **age and gender-specific organ system effects**.

The primary objective is to understand which organ systems are most affected by these drugs, particularly in relation to patient demographics. This information can be helpful in **drug safety monitoring** and **future formulation improvements**.

---

## **Drugs Analyzed**

1. **Tamoxifen (G)**

   * **Class:** Selective Estrogen Receptor Modulator (SERM)
   * **Use:** Treatment and prevention of hormone receptor-positive breast cancer.
   * **Mechanism:** Blocks estrogen action in breast tissue.

2. **Letrozole (G)**

   * **Class:** Aromatase inhibitor
   * **Use:** Postmenopausal breast cancer treatment.
   * **Mechanism:** Reduces estrogen production by inhibiting aromatase enzyme activity.

---

## **Data Source**

* **Dataset:** FDA Adverse Event Reporting System (**FAERS**)
* **Time Frame:** 1995 – 2024
* **Initial Columns:** Patient sex, age, weight, reactions, reasons, case ID, product name, etc.
* **Final Processed Columns:**

  * **`organ_system`** – Organ system affected (derived using BERT-based text classification).
  * **`female`** – Number of female cases.
  * **`male`** – Number of male cases.
  * **`age`** – Age or age range of affected patients.

---

## **Data Processing Workflow**

### **1. Raw Data Collection**

* Downloaded raw CSV files from FAERS dashboard for each drug.
* Raw files contained many irrelevant or duplicate columns.

### **2. Data Cleaning & Preprocessing**

* Removed missing values, duplicates, and outliers.
* Filtered only essential columns: `sex`, `age`, `weight`, `reactions`.
* Normalized gender representation to **male/female counts**.

### **3. Organ System Classification**

* Extracted drug reactions and classified them into corresponding **organ systems** using **BERT (via Gemini)**.
* Created a new column `organ_system` representing the affected organ system.

### **4. Age & Gender Segmentation**

* Grouped data by **age ranges** (e.g., `30-44`, `45-60`, etc.).
* Segregated cases based on **male** and **female** counts.

### **5. Final Dataset**

* The processed dataset provides a clear view of **drug effects by organ system, age, and gender**.

---

## **Key Observations**

✔ **Higher Incidence in Females:**
For both drugs, adverse effects were significantly more reported in females compared to males.

✔ **Age Group Most Affected:**
The highest number of reported cases occurred in **females aged 45–60 years**.

✔ **Potential for Drug Optimization:**
These findings suggest that **future drug formulations** could be adjusted to minimize adverse effects in this vulnerable demographic.

---

## **Project Structure**

```
├── raw_data/                # Original raw datasets from FAERS
│   ├── tamoxifen_raw.csv
│   └── letrozole_raw.csv
│
├── processed_data/          # Cleaned and processed datasets
│   ├── tamoxifen_processed.csv
│   └── letrozole_processed.csv
│
├── analysis/                # Jupyter/Colab notebooks and scripts
│   ├── xgboost_analysis.ipynb
│   └── organ_classification.py
│
└── README.md                # Project documentation
```

---

## **Machine Learning & Further Work**

* Applied **XGBoost** to predict which **organ system** might be affected based on `age`, `male`, and `female` counts.
* Future scope:

  * Improve prediction accuracy with **hyperparameter tuning** and **feature engineering**.
  * Incorporate additional features like **dosage** and **duration of drug use**.
  * Extend analysis to other related drugs.

---

## **Results Interpretation**

The final processed files show:

* **Each row** → An organ system affected, with corresponding **age group** and **male/female counts**.
* **Insights** can guide researchers and pharmaceutical companies in **drug safety assessment** and **formulation refinement**.

---

## **Acknowledgements**

* **Data Source:** [FAERS Dashboard](https://www.fda.gov/drugs/questions-and-answers-fdas-adverse-event-reporting-system-faers)
* **Text Classification:** BERT (via Google Gemini)
* **Analysis Tools:** Python, Pandas, XGBoost, Scikit-learn
