# 🛒 Maven Market Dashboard

An interactive **Power BI** dashboard analyzing the performance of **Maven Market**, a fictional grocery chain operating across **Canada, Mexico, and the USA**. The project covers revenue, profit, store and product performance, customer behavior, and returns, all in one report.

> **Tools:** Power BI Desktop · Power Query · DAX · Data Modeling (Star Schema)
> **Data source:** Maven Analytics – Maven Market dataset

---

## 📌 Table of Contents
1. [Project Overview](#-project-overview)
2. [Business Questions](#-business-questions)
3. [Dataset](#-dataset)
4. [Data Model](#-data-model)
5. [Data Preparation](#-data-preparation)
6. [Key DAX Measures](#-key-dax-measures)
7. [Dashboard Pages & Features](#-dashboard-pages--features)
8. [Key Insights](#-key-insights)
9. [How to Run](#-how-to-run)
10. [Repository Structure](#-repository-structure)
11. [Future Improvements](#-future-improvements)
12. [Author](#-author)

---

## 📖 Project Overview

Maven Market is a multi-country supermarket chain with stores across several regions. The goal of this project is to give management a single place to monitor business health and spot opportunities, by:

- Cleaning and combining multiple tables in **Power Query**
- Building a **star-schema** model around the transactions fact table
- Writing **DAX** measures for revenue, cost, profit, returns, and time intelligence
- Designing an interactive, multi-page **dashboard** with filters and drill-through

## ❓ Business Questions

- How much **revenue, profit, and quantity** is the company generating, and how is it trending?
- Which **stores, regions, and countries** perform best?
- Which **product brands, departments, and categories** are most profitable?
- What does the **customer base** look like (location, demographics, membership)?
- What are the **return rates**, and where are returns concentrated?
- How do results compare **period over period**?

## 🗂 Dataset

| Table | Type | Description |
|---|---|---|
| `Transactions` | Fact | Sales lines: date, product, customer, store, quantity |
| `Returns` | Fact | Returned items by date, product, and store |
| `Products` | Dimension | Product name, brand, retail price, cost, and attributes |
| `Customers` | Dimension | Customer location and demographic information |
| `Stores` | Dimension | Store name, type, location, and size |
| `Regions` | Dimension | Sales region, district, and country |
| `Calendar` | Dimension | Date table for time intelligence |

## 🧩 Data Model

A **star schema** with `Transactions` and `Returns` as fact tables, connected to the `Products`, `Customers`, `Stores`, `Regions`, and `Calendar` dimensions through one-to-many relationships.

```
Customers ──┐
Products ───┼──< Transactions >──┬── Calendar
Stores ─────┘                    └── Stores >── Regions
Products ──< Returns >── Stores
```

> 📷 *Add a screenshot of your model view:* `![Data Model](images/data_model.png)`

## 🧹 Data Preparation

Performed in **Power Query**:

- Verified and corrected data types
- Removed duplicates and handled null values
- Created calculated columns (e.g., full customer name, age, store size groups)
- Joined stores to regions for a clean geographic hierarchy
- Built a dedicated `Calendar` table and marked it as the date table

## 🧮 Key DAX Measures

```DAX
Total Revenue = SUMX(Transactions, Transactions[quantity] * RELATED(Products[product_retail_price]))

Total Cost = SUMX(Transactions, Transactions[quantity] * RELATED(Products[product_cost]))

Total Profit = [Total Revenue] - [Total Cost]

Profit Margin % = DIVIDE([Total Profit], [Total Revenue])

Total Transactions = COUNTROWS(Transactions)

Quantity Sold = SUM(Transactions[quantity])

Total Returns = SUM(Returns[quantity])

Return Rate = DIVIDE([Total Returns], [Quantity Sold])

Revenue LY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR('Calendar'[Date]))

Revenue YoY % = DIVIDE([Total Revenue] - [Revenue LY], [Revenue LY])
```

> Adjust column names to match your own model.

## 📊 Dashboard Pages & Features

**1. Executive Summary**
- KPI cards: Revenue, Profit, Profit Margin, Transactions, Return Rate
- Monthly revenue and profit trend
- Performance by country and region

**2. Store & Region Performance**
- Store ranking by revenue and profit
- Map view of sales by location
- Store type and size comparison

**3. Product Analysis**
- Revenue and profit by brand, department, and category
- Top and bottom products
- Returns by product

**4. Customer Analysis**
- Customers by country, gender, age group, and membership level
- Revenue contribution by customer segment

**Interactive features:** slicers (year, quarter, country, store), cross-filtering, drill-down, drill-through, tooltips, and bookmarks.

> 📷 *Add dashboard screenshots:*
> `![Summary](images/summary.png)`
> `![Stores](images/stores.png)`
> `![Products](images/products.png)`
> `![Customers](images/customers.png)`

## 💡 Key Insights

*Replace these with the findings from your own dashboard:*

- **Top market:** [e.g., USA generates X% of revenue]
- **Best stores:** [e.g., Store N leads in profit]
- **Top products:** [e.g., Brand X / Department Y drives most sales]
- **Trend:** [e.g., Revenue peaks in months X and Y]
- **Returns:** [e.g., Return rate is X%, highest in category Y]

## ▶️ How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   ```
2. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free, Windows).
3. Open `Maven_Market_Dashboard.pbix`.
4. If prompted, update the data source path: **Home → Transform data → Data source settings**.
5. Click **Refresh** to load the data.

## 📁 Repository Structure

```
├── Maven_Market_Dashboard.pbix   # Power BI report
├── data/                         # Source CSV files
├── images/                       # Screenshots of the dashboard and model
└── README.md
```

## 🚀 Future Improvements

- Add sales forecasting
- Add basket analysis to find products bought together
- Implement row-level security by region
- Publish to Power BI Service with scheduled refresh

## 👤 Author

**Seif Hussein Aboelazaim**
Computer Science & AI student at Cairo University (FCAI) · Aspiring Data Scientist
📧 seifhuss74@gmail.com · 🔗 [LinkedIn](https://linkedin.com/in/seifaboelazaim)
