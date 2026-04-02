# 📊 Superstore Sales Business Dashboard
### Data Analytics Portfolio Project — Power BI

---

## 🔗 Project Overview

An end-to-end business intelligence dashboard built on the Superstore Sales dataset.
Covers revenue trends, regional performance, product profitability, and customer segmentation
using Python for data cleaning and Power BI for interactive visualization.

**Tools Used:** Python (Pandas) · Power BI Desktop · DAX · Excel

**Dataset:** [Superstore Sales Dataset — Kaggle](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)

---

## 📁 Project Structure

```
superstore-dashboard/
│
├── data/
│   ├── Sample - Superstore.csv        ← Raw dataset (download from Kaggle)
│   └── superstore_cleaned.csv         ← Output after running cleaning script
│
├── superstore_cleaning.py             ← Python data cleaning script
├── Superstore_Dashboard.pbix          ← Power BI dashboard file
└── README.md                          ← This file
```

---

## 🧹 Step 1 — Data Cleaning (Python)

**Run the cleaning script:**
```bash
pip install pandas numpy
python superstore_cleaning.py
```

**What the script does:**
- Loads raw CSV with proper encoding
- Cleans column names (lowercase, no spaces)
- Converts date columns and extracts year, month, quarter, day
- Calculates shipping duration in days
- Removes duplicates
- Fills missing values
- Adds business metric columns: profit_margin_%, revenue_band, profit_flag
- Exports clean file ready for Power BI

---

## 📊 Step 2 — Power BI Dashboard

### How to Set Up

1. Download and install **Power BI Desktop** (free) from microsoft.com
2. Open Power BI → **Get Data** → Text/CSV → select `superstore_cleaned.csv`
3. Click **Transform Data** → verify column types → **Close & Apply**

---

### Dashboard Pages to Build

---

#### PAGE 1 — Executive Summary

**Visuals to add:**

| Visual Type | Fields to Use | Purpose |
|---|---|---|
| Card | SUM(sales) | Total Revenue |
| Card | SUM(profit) | Total Profit |
| Card | AVERAGE(profit_margin_%) | Avg Profit Margin |
| Card | COUNT(order_id) | Total Orders |
| Line Chart | order_year + order_month on X, SUM(sales) on Y | Revenue Trend Over Time |
| Donut Chart | category → SUM(sales) | Revenue by Category |
| Bar Chart | region → SUM(sales) | Revenue by Region |
| Slicer | order_year | Year Filter |

**DAX Measures to create (Home → New Measure):**
```
Total Revenue = SUM('superstore_cleaned'[sales])

Total Profit = SUM('superstore_cleaned'[profit])

Profit Margin = DIVIDE([Total Profit], [Total Revenue]) * 100

Total Orders = COUNTROWS('superstore_cleaned')

Avg Order Value = DIVIDE([Total Revenue], [Total Orders])
```

---

#### PAGE 2 — Regional Performance

**Visuals to add:**

| Visual Type | Fields | Purpose |
|---|---|---|
| Map Visual | state (location), SUM(sales) (bubble size) | Geographic Revenue Map |
| Clustered Bar | region → SUM(sales), SUM(profit) | Region Revenue vs Profit |
| Matrix Table | region → state → city → SUM(sales) | Drill-down regional table |
| Slicer | region | Filter by region |
| Slicer | order_year | Filter by year |

**DAX for this page:**
```
YoY Revenue Growth =
VAR CurrentYear = CALCULATE([Total Revenue], FILTER(ALL('superstore_cleaned'), 'superstore_cleaned'[order_year] = MAX('superstore_cleaned'[order_year])))
VAR PrevYear = CALCULATE([Total Revenue], FILTER(ALL('superstore_cleaned'), 'superstore_cleaned'[order_year] = MAX('superstore_cleaned'[order_year]) - 1))
RETURN DIVIDE(CurrentYear - PrevYear, PrevYear) * 100
```

---

#### PAGE 3 — Product & Category Analysis

**Visuals to add:**

| Visual Type | Fields | Purpose |
|---|---|---|
| Treemap | category → sub_category → SUM(sales) | Revenue breakdown by category |
| Horizontal Bar | Top 10 product_name → SUM(sales) | Top 10 Products by Revenue |
| Scatter Plot | SUM(sales) on X, SUM(profit) on Y, category as legend | Profit vs Revenue per product |
| Bar Chart | sub_category → SUM(profit) sorted descending | Most profitable sub-categories |
| Slicer | category | Filter by category |

**How to get Top 10 products:**
- Click the Bar Chart → click the filter icon → select Top N → Top 10 by SUM(sales)

---

#### PAGE 4 — Customer Segmentation

**Visuals to add:**

| Visual Type | Fields | Purpose |
|---|---|---|
| Bar Chart | segment → SUM(sales) | Revenue by customer segment |
| Line Chart | order_month_name → SUM(sales) by segment | Monthly trend by segment |
| Table | customer_name → SUM(sales) → SUM(profit) sorted | Top customers |
| Donut Chart | ship_mode → COUNT(order_id) | Shipping preference |
| Card | COUNTROWS of customer_id distinct | Total Unique Customers |

---

### Dashboard Design Tips

- **Color Theme:** Use a consistent 2–3 color palette. Recommended: Blue (#0066CC), Orange (#FF6B35), Grey (#F5F5F5 background)
- **Fonts:** Use Segoe UI throughout (Power BI default — clean and professional)
- **Layout:** Put KPI cards at the top, main chart in center, filters on the right side
- **Slicers:** Always add Year and Category slicers — shows interactivity to recruiters
- **Page Navigation:** Add buttons to navigate between pages (Insert → Buttons → Navigator)

---

## 💡 Key Business Insights (Write These in Your Resume/LinkedIn)

After building the dashboard, find and note these insights — you'll be asked about them in interviews:

1. Which region generates the most revenue but lowest profit margin?
2. Which product category has the highest return on sales?
3. Which month consistently shows the highest sales spike?
4. Which customer segment is most profitable?
5. Which products are high revenue but negative profit (loss leaders)?

**These 5 answers = your talking points in every interview.**

---

## 🚀 How to Share This Project

**Option 1 — GitHub (Must Do)**
- Export your Power BI file as `.pbix`
- Upload `.pbix`, `superstore_cleaning.py`, `README.md` to a GitHub repo
- Name the repo: `superstore-sales-dashboard`

**Option 2 — Power BI Service (Impressive)**
- Publish from Power BI Desktop → Power BI Service (free account)
- Share the live dashboard link on LinkedIn and resume

**Option 3 — LinkedIn Post**
- Take screenshots of your best dashboard page
- Post with this caption:
  *"Built an end-to-end sales analytics dashboard using Python + Power BI on the Superstore dataset. Key findings: [your 2–3 insights]. Open to Data Analyst opportunities. #DataAnalytics #PowerBI #Python"*

---

## 📝 Resume Description for This Project

```
Superstore Sales Business Dashboard | Python · Power BI · DAX
- Cleaned and transformed 10,000+ row retail dataset using Python (Pandas),
  engineering 6 new business metric columns including profit margin and revenue bands
- Built 4-page interactive Power BI dashboard covering executive KPIs, regional
  performance, product analysis, and customer segmentation
- Identified top-performing regions, seasonal revenue trends, and loss-making
  product categories using DAX measures and drill-through filters
```

---

*Project by [Your Name] | [Your LinkedIn URL] | [Your GitHub URL]*
