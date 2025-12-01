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
- Monthly Order Count vs Monthly Active Customers

<p align="center">
  <img src="images/Tableau 01a - Revenue Total Monthly .png" width="85%">
</p>

<p align="center">
  <img src="images/Tableau 01b - Customer vs Order Count.png" width="85%">
</p>

NorthStar shows strong seasonality: revenue peaks every November–December and drops in January–February.  
The 6-month rolling average trends upward from **$4.1M → $5.2M**, indicating stable long-term growth. 

<br><br>
---

### **2. Impact of Full Price vs Discounted Price **

**Key Metrics:**  
- Monthly Revenue from items purchased at Full Price VS Discounted Price
<br><br>
<p align="center">
  <img src="images/Tableau 02 - Discount vs Full Price Revenue .png" width="85%">
</p>

Customer count and order volume follow the same pattern, rising gradually across five years.  
Order frequency per active customer stays almost constant.
Growth comes mainly from **more customers**, not more purchases per customer.  

**Recommendation:**  

<br><br>
<p align="center">
  <img src="images/Tableau 01c - Discount vs Full Price Revenue .png" width="85%">
</p>

Q4 profits rely heavily on discounting: 
Every November and December each year show large discount spikes and weaker full-price revenue.
This may indicate inventory pressure earlier in the year which necessitate
heavy discounting to purge them out of inventory before holiday season is over.

**Recommendation:**  
- Shift from blanket discounts to targeted, data-driven promos.
- Test discount depth to identify optimal markdown levels by category.

<br><br>
---

### **3. Month-over-Month (MoM) Change**

**Key Metrics:**  
- Month Over Month revenue change.

<p align="center">
  <img src="images/Tableau 03 - Revenue MoM Change.png" width="85%">
</p>

MoM results show heavy seasonality: revenue spikes every November–December and then drops **50–70%** in January.  
Outside holiday periods, MoM growth is small and volatile.
Short-term momentum is inconsistent outside Q4, making the business highly dependent on holiday performance.

**Recommendation:**  

- Build stronger Q2–Q3 demand with targeted campaigns.
- Create NorthStar-branded “mini-peak” events outside holidays.
- Expand replenishment programs in Grocery, Beauty, and Baby.

<br><br>
---

### **4. New vs Returning Customers**

**Key Metrics:**  
- Revenue from new customers vs Revenue from repeat customers

<p align="center">
  <img src="images/Tableau 04 - Revenue from New VS Returning Customer Monthly.png" width="85%">
</p>

Growth is retention-driven, new customer acquisition is too small relative to total revenue and needs reinforcement.
Repeat customers generate the majority of revenue, while revenue from first-time customers declines over time.  
Holiday peaks are driven almost entirely by returning customers.

**Recommendation:** 

- Run new customers acquisition-focused campaigns in weak months, and improve onboarding to convert first-time buyers into repeat buyers faster.
- Launch referral programs driven by loyal returning customers.

<br><br>
---

### **5. Seasonality **

Key metrics:
- Revenue by Seasons

<p align="center">
  <img src="images/Tableau 05 - Revenue by Season.png" width="85%">
</p>

Fall and Winter consistently produce the highest revenue each year.  
Spring and Summer lag behind, with Spring typically the weakest season.

**Recommendation:** 
- NorthStar must plan for strong seasonality and focus on stabilizing demand in the first half of the year.
- Tighten Q2–Q3 demand forecasting.
- Add mid-season forecast checkpoints.
- Classify high-risk SKUs and markdown earlier instead of waiting for Q4.
  
<br><br>
---

### **6. Holiday & Event-Driven Revenue**

Key metrics:
-Revenue by US Holidays and Multicultural Holidays

<p align="center">
  <img src="images/Tableau 06 - Revenue by Holidays.png" width="85%">
</p>

Christmas season delivers the single largest revenue spike each year, followed by the Thanksgiving → Black Friday → Cyber Monday period.  
Multicultural NYC events (Diwali, Lunar New Year, Eid) generate smaller but reliable boosts.

**Recommendation:** 
U.S. retail holidays dominate the demand curve, while multicultural events offer steady but secondary uplift.

<br><br>
---

### **7. Channel Patterns**

Key metrics :
- Revenue VS Order Count by Sales Channel ( Quarterly )

<p align="center">
  <img src="images/Tableau 07a - Revenue VS Order Count by Sales Channel Quarterly .png" width="85%">
</p>

<p align="center" style="margin:30px 0;"></p>

<p align="center">
  <img src="images/Tableau 07b - Growth of Sales Channel .png" width="85%">
</p>

**Online** is the fastest-growing and highest-revenue channel. It is the core profit engine, outpacing the other channels.
**Store** remains large but shows slower growth.  
**Pickup** and **Delivery** remain small and mostly flat.

**Recommendation:** 
- NorthStar’s channel mix is shifting toward an online-first model, requiring continued investment in digital experience and fulfillment.
- Continue heavy investment in Online (core revenue + profit engine).
- Reevaluate Pickup/Delivery economics; adjust thresholds and fees.

<br><br>
---

### **8. Profit & Margin Quality Analysis**

Key metrics:
- Annual Gross Profit by each category
- Annual Gross Profit by each sales channel
- Annual Gross Profit by each customer segment

<p align="center">
  <img src="images/Tableau 08a - Gross Profit by Category.png" width="85%">
</p>

Margins are strong but concentrated and sensitive to inventory mistakes. 

The data show both strengths and vulnerabilities:
- High-margin categories drive most profit: **Clothing, Beauty, Toys, Sports**  
- Low-margin categories remain flat: **Grocery, Office, Home**

**Recommendation:** 
- Invest more in high-margin categories (Clothing, Beauty, Toys, Sports) to maximize profit growth.
- Improve efficiency in low-margin categories (Grocery, Office, Home) via vendor negotiation, pricing adjustments, or SKU reduction.
- Adjust or reposition weak categories (Grocery, Office, Home).
- Build curated bundles mixing high- and low-margin items.

<br><br>
<p align="center">
  <img src="images/Tableau 08b - Profit per Sales Channel .png" width="85%">
</p>

Pickup/Delivery contribute little profit and remain margin-stagnant.
  
**Recommendation:** 
- Expand and optimize Online + Store channels, which deliver the strongest profitability.
- Restructure Pickup/Delivery operations to reduce costs or reposition them as convenience services.
  
<br><br>
<p align="center">
  <img src="images/Tableau 08c - Profit per Customer Segment .png" width="85%">
</p>

Profit is overwhelmingly **Consumer-driven**; SMB/Enterprise play a minimal role .

**Recommendation:**  
- Focus marketing and loyalty programs on Consumer customers, the primary profit source.
- Plan growth strategies around discretionary spending patterns, where the business consistently performs best.
- Strengthen Consumer experience while exploring SMB/Enterprise expansion.

<br><br>
---



