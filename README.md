# 🏥 Healthcare Analytics Dashboard

> **An end-to-end Excel-based healthcare data analytics project analyzing 160,000 patient records across demographics, chronic conditions, insurance providers, and clinical registrations — designed to surface actionable healthcare insights through structured data modeling and interactive dashboards.**

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Business Problem & Objective](#-business-problem--objective)
- [Dataset Description](#-dataset-description)
- [Data Dictionary](#-data-dictionary)
- [Workbook Structure](#-workbook-structure)
- [Data Cleaning & Preprocessing](#-data-cleaning--preprocessing)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Key Insights](#-key-insights)
- [Dashboard Features](#-dashboard-features)
- [Tools & Technologies](#-tools--technologies)
- [Project Structure](#-project-structure)
- [How to Use](#-how-to-use)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 🔍 Project Overview

Healthcare organizations generate massive volumes of patient data daily. Without proper structure and analytics, this data remains underutilized — leading to missed clinical opportunities, inefficient resource allocation, and poor patient outcomes.

This project builds a **production-style patient master data system** using Microsoft Excel, analyzing **160,000 patient records** from 7 cities across Maharashtra, India. It covers the full analytics lifecycle: raw data ingestion → cleaning → transformation → EDA → insight generation → interactive dashboard.

The project is designed to demonstrate **real-world data analyst competencies** including data modeling, pivot-based reporting, derived metrics, and healthcare KPI tracking.

---

## 💼 Business Problem & Objective

### Problem Statement
A regional healthcare network needed a **centralized, analytically ready patient database** to:
- Understand patient demographics and health risk profiles
- Track chronic disease prevalence across cities and age groups
- Analyze insurance provider coverage and policy distributions
- Monitor patient registration trends over time (2020–2024)
- Enable clinical decision-making through data-driven insights

### Project Objective
> Build a **scalable, Excel-based analytics solution** that transforms raw patient records into structured insights and an interactive dashboard — enabling healthcare administrators to make faster, evidence-based decisions.

---

## 📦 Dataset Description

| Attribute | Details |
|-----------|---------|
| **Source** | Healthcare Analytics Dashboard (healthcare domain) |
| **Total Records** | 160,000 patients |
| **Total Fields** | 25 core attributes + 1 derived field |
| **Geographic Scope** | 7 cities — Maharashtra, India |
| **Time Period** | January 2020 – December 2024 |
| **Missing Data** | `Chronic_Condition` — 27,305 records (17.1%) |
| **Duplicate Records** | None detected |
| **File Format** | `.xlsx` (Excel Workbook) |

### Coverage Snapshot

| Dimension | Value |
|-----------|-------|
| Age Range | 25 – 66 years |
| Mean Age | 45.0 years |
| Gender Split | Male 50.1% / Female 49.9% |
| Blood Groups | 8 types (near-uniform distribution) |
| Chronic Conditions | 5 types |
| Insurance Providers | 6 providers |
| Cities Covered | 7 (Nagpur, Pune, Navi Mumbai, Nashik, Mumbai, Aurangabad, Kolhapur) |

---

## 📖 Data Dictionary

### Demographics & Identity

| Column | Type | Description |
|--------|------|-------------|
| `Patient_ID` | String | Unique patient identifier (P00001 – P20050 format) |
| `First_Name` | String | Patient first name |
| `Last_Name` | String | Patient last name |
| `Gender` | Categorical | Male / Female |
| `Age` | Integer | Age in years (25–66) |
| `Date_of_Birth` | Date | Birth date (YYYY-MM-DD) |
| `Marital_Status` | Categorical | Single / Married |

### Contact & Location

| Column | Type | Description |
|--------|------|-------------|
| `Phone_Number` | Integer | 10-digit mobile number |
| `Email` | String | Patient email address |
| `Address` | String | Street-level address |
| `City` | Categorical | One of 7 Maharashtra cities |
| `State` | String | Maharashtra (constant) |
| `Country` | String | India (constant) |
| `Pincode` | Integer | 6-digit postal code |

### Clinical & Health Metrics

| Column | Type | Description |
|--------|------|-------------|
| `Blood_Group` | Categorical | A+, A-, B+, B-, O+, O-, AB+, AB- |
| `Height_cm` | Integer | Height in centimetres |
| `Weight_kg` | Integer | Weight in kilograms |
| `BMI` | Float | Calculated Body Mass Index |
| `Smoking_Status` | Categorical | Yes / No |
| `Alcohol_Consumption` | Categorical | Yes / No / Occasionally |
| `Chronic_Condition` | Categorical | Asthma, Cardiac, Diabetes, Hypertension, Thyroid (17.1% null) |
| `Primary_Doctor_ID` | String | Assigned physician reference ID |

### Insurance & Administrative

| Column | Type | Description |
|--------|------|-------------|
| `Insurance_Provider` | Categorical | 6 providers (Star Health, HDFC Ergo, etc.) |
| `Insurance_Policy_No` | String | Unique policy reference number |
| `Registration_Date` | Date | Date of first registration (2020–2024) |

### Derived Field (Patient Data Sheet)

| Column | Type | Description |
|--------|------|-------------|
| `Age Between` | Categorical | Age bucketed into ranges: 25–35, 35–45, 45–55, 55–65, 65–75 |

---

## 🗂️ Workbook Structure

The Excel workbook is organized across **5 sheets**, each serving a distinct analytical purpose:

| Sheet Name | Purpose | Records |
|------------|---------|---------|
| `patient_master_1 (1)` | Primary raw data — first cohort | 20,000 |
| `patient2` | Extended raw data — second cohort | 140,000 |
| `Patient Data` | Cleaned & enriched master view (with `Age Between` grouping) | 160,000 |
| `Sheet2` | Pivot table summaries (Blood Group, City, Gender, Condition, Insurance, Age, Registrations) | Summary |
| `Sheet1` | Template / scratch working sheet | — |

---

## 🧹 Data Cleaning & Preprocessing

### Issues Identified & Resolved

- **Null values in `Chronic_Condition`** — 27,305 records (17.1%) had no recorded condition, indicating patients with no current diagnosis. Tagged as `"None Diagnosed"` in the analysis layer rather than imputed, to preserve clinical accuracy.
- **Inconsistent sheet splits** — Source data was split across two sheets (20K + 140K records). Consolidated into a unified `Patient Data` master sheet using structured references.
- **Data type standardization** — Dates (`Date_of_Birth`, `Registration_Date`) standardized to `YYYY-MM-DD` format across both cohorts.
- **BMI validation** — Cross-verified computed BMI against `Height_cm` and `Weight_kg` inputs. Flagged records with BMI below 14 or above 42 for clinical review.
- **Derived field creation** — `Age Between` column created using nested `IFS` logic to segment patients into 5-year age bands for pivot compatibility.
- **Zero duplicates detected** — Patient IDs confirmed unique across all 160,000 records.

### Data Quality Summary

| Check | Result |
|-------|--------|
| Duplicate Patient IDs | ✅ None found |
| Missing Demographics | ✅ 0 nulls |
| Missing Clinical Data (`Chronic_Condition`) | ⚠️ 27,305 (17.1%) — expected |
| Date Format Consistency | ✅ Standardized |
| BMI Range Validity | ✅ 14.0 – 42.2 (clinically plausible) |
| Outliers (Age) | ✅ None beyond defined range 25–66 |

---

## 📊 Exploratory Data Analysis

### 1. Age Distribution

| Age Band | Count | Share |
|----------|-------|-------|
| 25–35 | 37,913 | 23.7% |
| 35–45 | 40,033 | 25.0% |
| 45–55 | 40,087 | 25.1% |
| 55–65 | 37,782 | 23.6% |
| 65–75 | 4,185 | 2.6% |

> **Takeaway:** The dataset is dominated by working-age adults (35–55), representing 50.1% of all patients — a critical segment for preventive care programs.

### 2. Gender Distribution

| Gender | Count | Share |
|--------|-------|-------|
| Male | 80,223 | 50.1% |
| Female | 79,777 | 49.9% |

> **Takeaway:** Near-perfect parity, indicating a representative and unbiased patient base.

### 3. BMI Profile

| Metric | Value |
|--------|-------|
| Minimum | 14.0 |
| 25th Percentile | 21.2 |
| Median | 25.5 |
| 75th Percentile | 29.8 |
| Maximum | 42.2 |
| Mean | 25.8 |

> **Takeaway:** Median BMI of 25.5 sits at the Normal/Overweight boundary. The 75th percentile at 29.8 suggests a significant overweight population warranting lifestyle intervention.

### 4. Chronic Condition Breakdown

| Condition | Count | Share (of diagnosed) |
|-----------|-------|---------------------|
| Asthma | 27,319 | 20.5% |
| Thyroid | 27,300 | 20.5% |
| Hypertension | 27,213 | 20.4% |
| Diabetes | 27,209 | 20.4% |
| Cardiac | 23,654 | 17.7% |
| No Condition Recorded | 27,305 | — |

> **Takeaway:** Chronic conditions are uniformly distributed with no single dominant disease, suggesting a systemic public health challenge rather than a localized one.

### 5. Lifestyle Risk Factors

| Factor | Yes | No | Occasionally |
|--------|-----|----|-------------|
| Smoking | 79,948 (50.0%) | 80,052 (50.0%) | — |
| Alcohol | — | 79,620 (49.8%) | 80,380 (50.2%) |

> **Takeaway:** A 50% active smoking rate is a significant public health risk signal. Combined with 50.2% occasional alcohol consumers, lifestyle-linked disease burden is substantial across the cohort.

### 6. Insurance Provider Distribution

| Provider | Patients | Share |
|----------|----------|-------|
| Star Health | 27,537 | 17.2% |
| New India Assurance | 27,465 | 17.2% |
| HDFC Ergo | 27,366 | 17.1% |
| ICICI Lombard | 27,208 | 17.0% |
| Reliance General | 27,207 | 17.0% |
| Bajaj Allianz | 23,217 | 14.5% |

> **Takeaway:** Near-uniform market share across top 5 providers indicates a competitive insurance landscape. Bajaj Allianz shows slight under-penetration at 14.5%.

### 7. City-Level Distribution

| City | Patients | Share |
|------|----------|-------|
| Nagpur | 24,079 | 15.0% |
| Pune | 24,075 | 15.0% |
| Navi Mumbai | 24,036 | 15.0% |
| Nashik | 24,007 | 15.0% |
| Mumbai | 23,693 | 14.8% |
| Aurangabad | 20,151 | 12.6% |
| Kolhapur | 19,959 | 12.5% |

### 8. Registration Trend (Year-over-Year)

| Year | Registrations | YoY Change |
|------|--------------|------------|
| 2020 | 33,002 | — |
| 2021 | 33,576 | +1.7% |
| 2022 | 32,985 | -1.8% |
| 2023 | 33,534 | +1.7% |
| 2024 | 26,903 | -19.8%* |

*2024 reflects partial-year data (Jan–Dec 2024, data ends December 2024)

### 9. Monthly Registration Pattern

| Month | Registrations | Month | Registrations |
|-------|--------------|-------|--------------|
| January | 14,088 | July | 13,837 |
| February | 12,724 | August | 13,721 |
| March | 13,601 | September | 13,497 |
| April | 13,264 | October | 13,490 |
| May | 13,615 | November | 13,144 |
| June | 13,224 | December | 11,795 |

> **Takeaway:** January peaks and December troughs suggest seasonal registration cycles — likely tied to annual health check-up programs and end-of-year slowdowns.

---

## 💡 Key Insights

### 🏥 Clinical Insights
- **Chronic condition gap:** 17.1% of patients have no recorded diagnosis — may indicate data capture gaps or genuinely healthy individuals requiring dedicated tracking.
- **Equal disease burden:** Asthma, Thyroid, Hypertension, and Diabetes each affect ~20% of diagnosed patients — signaling a multi-disease management challenge across the network.
- **BMI concern:** The 25th–75th percentile range (21.2–29.8) means a large middle band of patients is at elevated metabolic risk with relatively normal-looking averages.

### 📍 Operational Insights
- **Geographic parity:** Patient load is well-distributed across 7 cities, suggesting uniform service delivery capacity — but Aurangabad and Kolhapur (12.5–12.6%) may be underserved relative to larger metros.
- **Stable registrations:** Four consistent years of ~33K registrations indicates a mature, stable patient acquisition funnel.
- **January surge:** 14,088 January registrations (highest monthly figure) suggests front-loaded health program enrollments — an opportunity for targeted outreach and capacity planning.

### 💰 Insurance Insights
- **Bajaj Allianz under-coverage:** At 14.5% vs. ~17% for peers, Bajaj Allianz represents the lowest market penetration — a potential coverage gap or partner expansion opportunity.
- **100% insurance coverage:** Every patient record has an insurance provider assigned, indicating this dataset covers an insured population — a key data limitation to note for broader population studies.

### ⚠️ Risk Flags
- 50% smoking prevalence combined with widespread chronic conditions (Cardiac: 23,654 patients) creates a compounding risk profile across the entire cohort.
- Blood group distribution is near-uniform (~20,000 each) — clinically unusual and should be validated against source data for randomization artifacts.

---

## 📊 Dashboard Features

The Excel workbook includes a **pivot-table-driven analytics layer** with the following summary views:

| Dashboard Element | Description |
|------------------|-------------|
| 📋 **Total Patient Count** | Top-line KPI card — 160,000 records |
| 👥 **Gender Split** | Male vs. Female count and percentage |
| 🩸 **Blood Group Distribution** | Count across all 8 blood types |
| 📍 **City-wise Patient Volume** | Breakdown across 7 Maharashtra cities |
| 🎂 **Age Group Segmentation** | 5 age bands (25–35 through 65–75) |
| 🚬 **Smoking Status** | Yes / No breakdown with marital status cross-tab |
| 🍷 **Alcohol Consumption** | No / Occasionally breakdown by marital status |
| 🏥 **Chronic Condition Frequency** | Condition-wise patient counts |
| 🛡️ **Insurance Provider Split** | Patient count per provider |
| 📅 **Year-on-Year Registrations** | 2020–2024 registration trend |
| 📆 **Monthly Registration Volume** | Seasonal registration pattern (Jan–Dec) |

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|------|-------|
| **Microsoft Excel** | Primary platform — data storage, transformation, visualization |
| **Pivot Tables & Pivot Charts** | Multi-dimensional aggregation and cross-tabulation |
| **Excel Formulas** | `IF`, `IFS`, `COUNTIF`, `AVERAGEIF`, `ISNULL`, `TEXT`, `DATEDIF` for derived fields |
| **Data Validation** | Dropdown constraints for categorical field integrity |
| **Conditional Formatting** | Visual flags for BMI ranges and data quality issues |
| **Named Ranges** | Structured references for scalable pivot table connections |
| **Excel Slicers** | Interactive filtering on pivot dashboards |

---

## 📁 Project Structure

```
patient-master-analytics/
│
├── 📊 patient_data.xlsx                  ← Main Excel workbook (all sheets)
│   ├── patient_master_1 (1)             ← Raw data cohort 1 (20,000 records)
│   ├── patient2                         ← Raw data cohort 2 (140,000 records)
│   ├── Patient Data                     ← Cleaned + enriched master sheet (160,000)
│   ├── Sheet2                           ← Pivot table analytics layer
│   └── Sheet1                           ← Working / template sheet
│
├── 📄 README.md                         ← Project documentation (this file)
│
├── 📁 docs/
│   ├── data_dictionary.md              ← Field-level definitions
│   └── analysis_notes.md              ← Methodology and assumptions
│
└── 📁 exports/
    └── patient_data_cleaned.csv        ← CSV export for downstream tools
```

---

## 🚀 How to Use

### Prerequisites
- Microsoft Excel 2016 or later *(recommended)*
- Alternatively: Google Sheets or LibreOffice Calc

### Step-by-Step

**1. Open the workbook**
```
Open patient_data.xlsx in Microsoft Excel
```

**2. Navigate to the master data sheet**
```
Go to the "Patient Data" tab — the cleaned, enriched, analysis-ready master table
```

**3. Explore pivot summaries**
```
Open "Sheet2" to view pre-built pivot tables covering:
  - Demographics (Gender, Age Group, Blood Group)
  - Clinical (Chronic Conditions, Smoking, Alcohol)
  - Administrative (Insurance Providers, Cities, Registration Trends)
```

**4. Filter & slice the data**
```
Use Excel Slicers to dynamically filter by:
  City | Year | Age Group | Gender | Condition | Insurance Provider
```

**5. Export for external tools (optional)**
```python
import pandas as pd

df = pd.read_excel("patient_data.xlsx", sheet_name="Patient Data")
print(df.shape)          # (160000, 26)
print(df.columns.tolist())
df.to_csv("exports/patient_data_cleaned.csv", index=False)
```

---

## 🔮 Future Improvements

| Priority | Enhancement |
|----------|------------|
| 🔴 **High** | Migrate to Power BI for interactive drill-through dashboards with dynamic filters |
| 🔴 **High** | Add doctor-level performance analysis linking `Primary_Doctor_ID` to patient load and outcomes |
| 🟡 **Medium** | Integrate Power Map / Tableau for geographic heatmaps across Maharashtra cities |
| 🟡 **Medium** | Add derived BMI classification column (`Underweight / Normal / Overweight / Obese`) |
| 🟡 **Medium** | Build year-over-year registration growth rate as a calculated column |
| 🟢 **Low** | Implement Python EDA pipeline (pandas + seaborn) for reproducible statistical reporting |
| 🟢 **Low** | Design a normalized SQL schema for this dataset to enable database-layer analytics |
| 🟢 **Low** | Add re-registration / patient retention tracking for longitudinal cohort analysis |

---

## 👤 Author

**[Aman Mulani]**
*Data Analyst | Healthcare Analytics | Excel & Python*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat-square&logo=linkedin)]([https://linkedin.com/in/aman-mulani111/])
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat-square&logo=github)](https://github.com/theamanmulani).

---

> 💡 *If this project helped you or gave you ideas, consider giving it a ⭐ — it helps others discover it too.*

---

*Last updated: April 2026 · Records: 160,000 · Tool: Microsoft Excel · Domain: Healthcare Analytics*
