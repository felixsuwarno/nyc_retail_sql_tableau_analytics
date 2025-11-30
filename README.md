# nyc_retail_sql_tableau_analytics
A 5-year retail analytics case study using PostgreSQL + Tableau, modeling revenue, customers, profitability, and seasonality for a fictitious NYC-based omnichannel retailer (NorthStar).


# NorthStar NYC Retail — 5-Year Customer & Sales Analytics (PostgreSQL and Tableau visualization)

---

## 1. Project Overview

This project simulates a large omnichannel retailer serving the New York City metropolitan area between 2020–2024.  
Think of a NYC-focused version of **Target, Walmart, or Costco**.

The goal is to demonstrate real-world SQL analytics workflows, including:

- Core revenue & order trend analysis
- Month-over-month (MoM) revenue movement
- New vs returning customer revenue behavior
- Seasonal and holiday-driven demand patterns
- Multicultural NYC event effects (Diwali, Lunar New Year, Eid)
- Category-level gross profit analysis
- Discount vs full-price revenue impact
- Profitability by sales channel and customer segment
- Advanced SQL techniques (joins, aggregations, window functions)
- Dimensional modeling with a retail star schema (orders, order_items, customers, products, calendar)


All data is synthetic but designed to behave like real NYC retail patterns — including holiday spikes and multicultural demand cycles.

---

## 2. Business Scenario

NorthStar Retail operates across all major NYC and nearby regions:

- Manhattan  
- Brooklyn  
- Queens  
- Bronx  
- Staten Island  
- New Jersey Metro (Hudson, Bergen, Essex, Passaic)  
- Westchester / Long Island corridors  

Customers shop across four channels:

- Online  
- Store  
- Pickup  
- Delivery  

The retailer sells **10,000 products** across **9 major departments**:

Electronics, Home, Grocery, Clothing, Beauty, Sports, Toys, Office, Baby.

The dataset covers 2020–2024 and includes both U.S. and multicultural NYC seasonal effects:  
**Thanksgiving, Black Friday → Cyber Monday, Christmas season, Diwali, Lunar New Year, Eid**, federal holidays, and back-to-school.

---

## 3. Data Model (Star Schema)

### ⭐ Fact Table — order_items (line-item fact)  
One row per SKU per order.  
Includes: `order_item_id`, `order_id`, `product_id`, `quantity`, `list_price`, `discount_pct`, `net_price`, `line_revenue`.

### ⭐ Associated Fact — orders (header)  
Includes: `order_id`, `customer_id`, `order_date`, `sales_channel`, `order_status`.

### ⭐ Dimensions

**customers:** `customer_id`, region, segment, signup_date  
**products:** `product_id`, category, subcategory, unit_cost, list_price  
**dim_calendar:** date, Y/M/Q, seasons, holidays, fiscal fields

---

## 4. Schema Summary

customers (dim)
products (dim)
orders (fact header)
order_items (fact detail)
dim_calendar (dim)


Enables: LTV, retention, KPIs, seasonal uplift, category performance, and time-series analysis through window functions.

---
## ⭐ 5. Tech Stack

- **PostgreSQL** — window functions, joins, aggregations  
- **Tableau Public** — dashboards, KPI charts  
- **dbdiagram.io** — ERD & star-schema modeling  
- **Excel / Google Sheets** — QA & exploration  

---

## ⭐ 6. Skills Demonstrated

- SQL window functions (LAG, LEAD, rolling averages)  
- MoM, QoQ, Y/Y trend analysis  
- Cohort & retention modeling  
- LTV computation  
- Profit & margin modeling  
- Discount mix analysis  
- Seasonal & holiday uplift analysis  
- Star schema design  
- SQL performance tuning  
- Data storytelling for business stakeholders  

---

## 7. Business Questions & Insights

## 7. Profit & Margin Quality Analysis

- **High-margin categories drive most profit.**  
  Clothing, Beauty, Toys, Sports show strong margin contribution; Grocery, Office, Home remain small and flat.

- **Holiday profits rely heavily on discounting.**  
  In December 2023–2024, discounted revenue spikes while full-price revenue drops — clear signal of **inventory pressure earlier in the year** (overestimation, late shipments, or macro slowdowns).

- **Online is the primary profit engine**, outpacing Store and far exceeding Pickup/Delivery.

- **Pickup/Delivery remain low-margin and stagnant.**  
  Useful for convenience but not margin-accretive.

- **Profit is overwhelmingly Consumer-driven.**  
  SMB/Enterprise segments produce minimal incremental profit.

**Overall:** Margin quality is strong but concentrated and exposed to inventory risks and seasonal discount dependence.

---

# 8. Business Recommendations

### 8.1. Reduce Q4 Dependence
- Build stronger Q2–Q3 demand with targeted campaigns.  
- Create NorthStar-branded “mini-peak” events outside holidays.  
- Expand replenishment programs in Grocery, Beauty, and Baby.

### 8.2. Strengthen New Customer Acquisition
- Run acquisition-focused campaigns in weak months.  
- Launch referral programs driven by loyal returning customers.  
- Improve onboarding to convert first-time buyers into repeat buyers faster.

### 8.3. Increase Order Frequency per Customer
- Use recency-based lifecycle segments (Active, At-risk, Dormant).  
- Push cross-sell in high-margin categories (Beauty, Clothing, Toys, Sports).

### 8.4. Improve Pricing & Discount Strategy
- Avoid “panic markdowns” in December by starting earlier markdown cadence for slow movers.  
- Shift from blanket discounts to targeted, data-driven promos.  
- Test discount depth to identify optimal markdown levels by category.

### 8.5. Reduce Inventory Risk
- Tighten Q2–Q3 demand forecasting.  
- Add mid-season forecast checkpoints.  
- Classify high-risk SKUs and markdown earlier instead of waiting for Q4.

### 8.6. Channel Optimization
- Continue heavy investment in Online (core revenue + profit engine).  
- Reevaluate Pickup/Delivery economics; adjust thresholds and fees.  
- Use stores as omnichannel hubs (BOPIS with in-store cross-sell).

### 8.7. Category Strategy
- Double down on high-margin hero categories.  
- Adjust or reposition weak categories (Grocery, Office, Home).  
- Build curated bundles mixing high- and low-margin items.

### 8.8. Customer Segment Strategy
- Strengthen Consumer experience while exploring SMB/Enterprise expansion.  
- Pilot business accounts, bulk order options, and scheduled delivery.

### 8.9. Analytics & Experimentation Roadmap
- Build a formal test-and-learn framework for pricing and promos.  
- Develop a retention & churn monitoring dashboard.  
- Incorporate LTV into marketing spend decisions.

---
