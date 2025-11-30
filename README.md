# nyc_retail_sql_tableau_analytics
A 5-year retail analytics case study using PostgreSQL + Tableau, modeling revenue, customers, profitability, and seasonality for a fictitious NYC-based omnichannel retailer (NorthStar).


# NorthStar NYC Retail — 5-Year Customer & Sales Analytics (PostgreSQL and Tableau visualization)

<br><br>
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

<br><br>
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

<br><br>
---

## 3. Data Model (Star Schema)

### Fact Table — order_items (line-item fact)  
One row per SKU per order.  
Includes: `order_item_id`, `order_id`, `product_id`, `quantity`, `list_price`, `discount_pct`, `net_price`, `line_revenue`.

### Associated Fact — orders (header)  
Includes: `order_id`, `customer_id`, `order_date`, `sales_channel`, `order_status`.

### Dimensions

**customers:** 
`customer_id`, region, segment, signup_date  

**products:** 
`product_id`, category, subcategory, unit_cost, list_price  

**dim_calendar:** 
date, Y/M/Q, seasons, holidays, fiscal fields

<br><br>
---

## 4. Schema Summary

customers (dim)
products (dim)
orders (fact header)
order_items (fact detail)
dim_calendar (dim)


Enables: LTV, retention, KPIs, seasonal uplift, category performance, and time-series analysis through window functions.

<br><br>
---
## 5. Tech Stack

- **PostgreSQL** — window functions, joins, aggregations  
- **Tableau Public** — dashboards, KPI charts  

<br><br>
---

## 6. Skills Demonstrated

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

<br><br>
---

## 7. Business Questions & Insights


Below are the seven business questions analyzed using SQL + Tableau.

### **1. Monthly Revenue, Customer, and Order Trends (2020–2024)**

**Key Metrics:**  
- Monthly Revenue vs 6-Month Rolling Average  
- Monthly Orders vs Monthly Active Customers

<p align="center">
  <img src="images/Tableau 01a - Revenue Total Monthly .png" width="85%">
</p>

NorthStar shows strong seasonality: revenue peaks every November–December and drops in January–February.  
The 6-month rolling average trends upward from **$3.9M → $5.8M**, indicating stable long-term growth.  
Customer count and order volume follow the same pattern, rising gradually across five years.  
Order frequency per active customer stays almost constant.

**Overall:**  
Growth comes mainly from **more customers**, not more purchases per customer.  
The business is heavily dependent on Q4 and should encourage off-season purchases to reduce seasonal risk.

<br><br>
---

### **2. Month-over-Month (MoM) Change**

MoM results show heavy seasonality: revenue spikes every November–December and then drops **50–70%** in January.  
Outside holiday periods, MoM growth is small and volatile.

**Overall:**  
Short-term momentum is inconsistent outside Q4, making the business highly dependent on holiday performance.

<br><br>
---

### **3. New vs Returning Customers**

Repeat customers generate the majority of revenue, while revenue from first-time customers declines over time.  
Holiday peaks are driven almost entirely by returning customers.

**Overall:**  
Growth is retention-driven. Acquisition is too small relative to total revenue and needs reinforcement.

<br><br>
---

### **4. Seasonality (High / Low Months)**

Fall and Winter consistently produce the highest revenue each year.  
Spring and Summer lag behind, with Summer typically the weakest season.

**Overall:**  
NorthStar must plan for strong seasonality and focus on stabilizing demand in the first half of the year.

<br><br>
---

### **5. Holiday & Event-Driven Revenue**

Christmas season delivers the single largest revenue spike each year, followed by the Thanksgiving → Black Friday → Cyber Monday period.  
Multicultural NYC events (Diwali, Lunar New Year, Eid) generate smaller but reliable boosts.

**Overall:**  
U.S. retail holidays dominate the demand curve, while multicultural events offer steady but secondary uplift.

<br><br>
---

### **6. Channel Patterns**

**Online** is the fastest-growing and highest-revenue channel.  
**Store** remains large but shows slower growth.  
**Pickup** and **Delivery** remain small and mostly flat.

**Overall:**  
NorthStar’s channel mix is shifting toward an online-first model, requiring continued investment in digital experience and fulfillment.

<br><br>
---

### **7. Profit & Margin Quality Analysis**

Margin insights show both strengths and vulnerabilities:

- High-margin categories drive most profit: **Clothing, Beauty, Toys, Sports**  
- Low-margin categories remain flat: **Grocery, Office, Home**  
- Q4 profits rely heavily on discounting: December 2023–2024 show large discount spikes and weaker full-price revenue → indicates inventory pressure earlier in the year  
- **Online** is the core profit engine, outpacing Store, Pickup, Delivery  
- Pickup/Delivery contribute little profit and remain margin-stagnant  
- Profit is overwhelmingly **Consumer-driven**; SMB/Enterprise play a minimal role  

**Overall:**  
Margins are strong but concentrated and sensitive to inventory mistakes.  
NorthStar must manage Q2–Q3 inventory more carefully and reduce reliance on markdown-heavy Q4 performance.

<br><br>
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
