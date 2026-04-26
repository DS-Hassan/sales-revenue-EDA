# 📊 Sales & Revenue Exploratory Data Analysis (EDA)

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-green?style=for-the-badge&logo=pandas)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

> **A full end-to-end exploratory data analysis on a real-world style B2B Sales dataset — from raw messy data to actionable business insights.**

---

## 🧠 Project Overview

This project simulates a real-world data analysis workflow. Starting with a deliberately **messy, uncleaned dataset**, I performed a complete EDA pipeline covering data cleaning, outlier detection, missing value handling, and multi-level analysis to surface key business insights for a fictional B2B sales company.

The dataset contains **1,000 sales orders** across multiple regions, sales reps, product categories, and channels — with intentional data quality issues mirroring what analysts encounter in production environments.

---

## 🎯 Business Questions Answered

| # | Question | Answer |
|---|----------|--------|
| 1 | Which region generates the most revenue per deal? | **South ($52,222 avg)** |
| 2 | Who is the top performing sales rep? | **Aisha Patel ($58,419 avg)** |
| 3 | Which product category drives the most revenue? | **Subscriptions ($53,240 avg)** |
| 4 | Which sales channel is most effective? | **Direct ($50,000 avg)** |
| 5 | What is the company's overall win rate? | **~43% — below healthy benchmark** |
| 6 | Which region has the highest win rate? | **East (55%) — most efficient closer** |
| 7 | Does discounting increase revenue? | **No — weak negative correlation (-0.077)** |
| 8 | What drives revenue the most? | **Quantity sold (correlation: 0.60)** |

---

## 📁 Project Structure

```
📦 Sales-Revenue-EDA
 ┣ 📄 sales_revenue.csv               ← Raw messy dataset (1,000 rows)
 ┣ 📓 eda_analysis.ipynb              ← Main Jupyter notebook
 ┣ 📄 pandas_complete_cheatsheet.py   ← Full pandas reference sheet
 ┗ 📄 README.md                       ← You are here
```

---

## 🗂️ Dataset Description

| Column | Type | Description |
|--------|------|-------------|
| `Order_ID` | String | Unique order identifier |
| `Order_Date` | DateTime | Date the order was placed |
| `Region` | Categorical | Geographic sales region |
| `Sales_Rep` | Categorical | Name of the sales representative |
| `Product_Category` | Categorical | Type of product sold |
| `Product_Name` | Categorical | Specific product name |
| `Customer_Segment` | Categorical | Enterprise / SMB / Startup |
| `Quantity` | Integer | Units sold per order |
| `Unit_Price` | Float | Price per unit ($) |
| `Discount_Rate` | Float | Discount applied (0–35%) |
| `Revenue` | Float | Total revenue generated ($) |
| `Deal_Status` | Categorical | Won / Lost / Pending |
| `Channel` | Categorical | Direct / Online / Partner / Referral |

---

## 🧹 Data Quality Issues Found & Fixed

The raw dataset contained **4 types of intentional mess** — all resolved during cleaning:

### 1. Missing Values
| Column | Missing Count | Missing % | Fix Applied |
|--------|--------------|-----------|-------------|
| Discount_Rate | 77 | 7.7% | Filled with mean |
| Customer_Segment | 63 | 6.3% | Filled with mode |
| Deal_Status | 69 | 6.9% | Filled with mode |
| Region | 52 | 5.2% | Filled with mode |
| Sales_Rep | 52 | 5.2% | Filled with mode |
| Revenue | 39 | 3.9% | Filled with mean |
| Channel | 39 | 3.9% | Filled with mode |

### 2. Inconsistent Formatting
- `Region`: `north`, `NORTH`, `North` → standardized to `North`
- `Deal_Status`: `won`, `WON`, `In Progress` → standardized to `Won`, `Pending`
- `Customer_Segment`: `enterprise`, `ENTERPRISE`, `start-up` → standardized to `Enterprise`, `Startup`
- `Channel`: `direct`, `DIRECT`, `referral` → standardized to `Direct`, `Referral`
- `Order_Date`: 5 mixed date formats → converted to `datetime64` using `format='mixed'`

### 3. Outliers Detected & Removed (IQR Method)
| Column | Issue | Action |
|--------|-------|--------|
| Quantity | Min: -5, Max: 9,999 | Removed negatives + IQR upper bound |
| Unit_Price | Min: -$50, Max: $150,000 | Removed negatives + IQR upper bound |
| Revenue | Min: -$1,000, Max: $9,999,999 | Removed negatives + IQR upper bound |

### 4. Duplicates
- **40 duplicate rows** identified and removed

### Dataset Size After Cleaning
| Stage | Rows |
|-------|------|
| Raw | 1,000 |
| After duplicate removal | 960 |
| After outlier removal | 876 |
| After missing value handling | **914** ✅ |

---

## 📈 Key Findings & Business Insights

### 💰 Revenue Distribution
- Most deals are **small to medium** ($13K–$78K range)
- Typical deal size: **$38,361** (median)
- Distribution is **right-skewed** — a few high-value deals pull the average up
- Average deal value: **$48,975**

### 🗺️ Regional Performance
- **South** generates the highest average revenue per deal ($52,222) despite fewer deals
- **Central** is the weakest region — lowest average revenue ($44,320)
- **North** has the most deals but only a **45% win rate** — high volume, lower efficiency
- **East** has the highest win rate at **55%** — fewest deals but closes them most effectively

### 👥 Sales Rep Performance
- **Top Rep:** Aisha Patel — $58,419 average revenue (fewest deals but highest value)
- **Lowest:** Mia Fernandez — $37,193 average revenue
- $21,226 gap between top and bottom rep — significant performance disparity

### 📦 Product Category Insights
- **Subscriptions** generate the highest average revenue per deal ($53,240)
- **Services** generates the least ($44,238) — potential pricing review needed
- All categories have similar deal volumes — revenue difference is about deal quality, not quantity

### 📣 Channel Effectiveness
- **Direct** channel: highest revenue per deal + second most volume — strongest channel overall
- **Referral**: fewest deals AND lowest revenue per deal — underperforming on both metrics
- Recommendation: invest more in Direct, review and revamp Referral strategy

### 🏆 Win Rate Analysis
- Overall win rate: **~43%** — below the healthy benchmark of 50%+
- Best region by win rate: **East (55%)**
- Worst region by win rate: **North (45%)**

### 🔗 Correlation Analysis
| Relationship | Correlation | Meaning |
|-------------|-------------|---------|
| Quantity ↔ Revenue | **+0.60** | Moderate positive — sell more units, make more money |
| Unit_Price ↔ Revenue | +0.13 | Weak positive |
| Discount_Rate ↔ Revenue | **-0.077** | Slight negative — more discounts = less revenue |

> **Key Takeaway:** The primary lever for growing revenue is **selling more units**, not adjusting price or discounts.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Python 3.10+** | Core programming language |
| **Pandas** | Data manipulation and analysis |
| **NumPy** | Numerical operations |
| **Matplotlib** | Base visualizations |
| **Seaborn** | Statistical visualizations |
| **Jupyter Notebook** | Interactive analysis environment |

---

## 🚀 How to Run This Project

```bash
# 1. Clone the repository
git clone https://github.com/DS-Hassan/sales-revenue-eda.git
cd sales-revenue-eda

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# 3. Launch Jupyter Notebook
jupyter notebook eda_analysis.ipynb
```

---

## 💡 Skills Demonstrated

- ✅ Real-world **data cleaning** (nulls, duplicates, outliers, formatting)
- ✅ **Statistical analysis** (IQR, correlation, distribution analysis)
- ✅ **Univariate, Bivariate & Multivariate** analysis
- ✅ **Data visualization** (histograms, box plots, bar charts, heatmaps)
- ✅ **Business thinking** — translating data findings into actionable insights
- ✅ **Python & Pandas** proficiency
- ✅ Clean, documented, reproducible code

---

## 📬 Contact

**Hassan**
📧 abdulehassan5@gmail.com
🔗 [LinkedIn](linkedin.com/in/hassan-abdule)| [GitHub](https://github.com/DS-Hassan)

---

> *"Data is only as good as the questions you ask it."*
> This project was built to answer the right questions. 🎯
