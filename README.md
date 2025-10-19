# Company_Financials

#  Finance Data Analytics Project — Python, SQL & Power BI

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-MySQL-orange?logo=mysql&logoColor=white)
![PowerBI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?logo=power-bi&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

##  Overview
This project explores the financial performance of various business segments using **Python**, **SQL**, and **Power BI**.  
The objective was to clean, analyze, and visualize financial data to understand how **profit** is influenced by **sales, cost, and discounts**.

We started from a raw Kaggle dataset and built a fully cleaned, analysis-ready version.  
Finally, we connected it to SQL and Power BI for interactive insights and business storytelling.

---

##  Dataset Description

| Column | Description |
|---------|-------------|
| `Segment` | Business segment (e.g., Government, Midmarket, etc.) |
| `Country` | Region of operation |
| `Product` | Product name |
| `Units_Sold` | Number of units sold |
| `Manufacturing_Price` | Cost to produce one unit |
| `Sale_Price` | Selling price per unit |
| `Gross_Sales` | Total sales before discounts (`Units_Sold × Sale_Price`) |
| `Discounts` | Discounts applied to Gross Sales |
| `Sales` | Net revenue after discounts (`Gross_Sales - Discounts`) |
| `COGS` | Cost of goods sold (`Units_Sold × Manufacturing_Price`) |
| `Profit` | Net profit (`Sales - COGS`) |
| `Date`, `Month_Number`, `Month_Name`, `Year` | Transaction time data |

---

##  Step 1 — Data Cleaning (Python)

###  Key Cleaning Steps
- Removed leading/trailing spaces in column names  
- Replaced spaces with underscores (SQL-friendly names)  
- Removed `$`, commas, and parentheses from numeric columns  
- Handled **negative values** in parentheses like `(1,200)` → `-1200`  
- Converted all numeric columns to `float64`  
- Parsed `Date` column into datetime format  
- Added a `Year_Month` column for time-based analysis  

###  Output
`Financials_Cleaned.csv` — a clean, consistent dataset ready for SQL and Power BI.

---

##  Step 2 — Exploratory Data Analysis (EDA)

We examined how **Profit** interacts with other numeric fields to understand what drives business success.

| Variable | Relationship with Profit | Description |
|-----------|--------------------------|--------------|
| `Sales` | Strong positive (+0.95) | More sales → higher profit |
| `Gross_Sales` | Very strong positive | Major revenue driver |
| `Discounts` | Moderate negative (-0.50) | More discounts → less profit |
| `COGS` | Slight positive | Reflects scale of operations |
| `Units_Sold` | Positive | Selling more units boosts total profit |

###  Core Formula

Profit = (Gross_Sales - Discounts) - COGS

##  Step 3 — Visualizations (Seaborn + Matplotlib)

### Correlation Heatmap
Shows how each metric relates to others.  
Profit is **highly correlated** with Sales and Gross Sales, and **negatively correlated** with Discounts.

### Pairplot
Gives an overview of how all numeric columns interact visually.

### Scatter Plots (Profit vs Variables)
- Profit vs **Sales** → strong upward trend  
- Profit vs **Discounts** → downward slope  
- Profit vs **COGS** → moderate relationship  
- Profit vs **Units Sold** → strong positive correlation  

###  Profit Margin Distribution

df['Profit_Margin_%'] = (df['Profit'] / df['Sales']) * 100

Shows efficiency of operations and cost control.

###  Segment-wise Scatter

sns.scatterplot(data=df, x='Discounts', y='Profit', hue='Segment')

##  Step 4 — Negative Profit Detection

During cleaning, we discovered **5 loss-making transactions** — originally recorded with parentheses in the raw file.  
After fixing, they appear correctly as negative floats:

| Country | Product | Profit |
|----------|----------|--------|
| USA | Montana | -4533.75 |
| USA | Paseo | -3740.00 |
| France | Paseo | -2981.25 |
| USA | Paseo | -1076.25 |
| France | Paseo | -880.00 |

 Ensures accurate reporting and correct profit analysis.


