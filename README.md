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

**SQL Analytics**
- SQL window functions (LAG, rolling averages)
- Month-over-Month, Quarter-over-Quarter, and Year-over-Year trend analysis
- Profit and gross margin analysis by category, sales channel, and customer segment
- Discount vs full-price revenue mix analysis
- Seasonal and holiday uplift analysis
- New vs returning customer revenue modeling

**Tableau Visualization**
- Multi-sheet dashboard composition
- Dual-axis charts (e.g., full-price vs discounted revenue)
- Trend lines and long-term forecasting visuals
- Continuous vs discrete date handling
- Custom color encoding (MoM positive/negative, customer type, category)
- Sorting across pane-level categories
- Table calculations (percent change, rolling averages)
- Facet charts by category, channel, and segment
- Measure Names / Measure Values for multi-metric views
- Clear labeling, axis formatting, and data-storytelling driven layout

**Business Analytics**
- Actionable insights for category strategy, pricing, customer acquisition, and retention
- Identification of growth engines, low-margin risks, and demand cyclicality
- Executive-level narrative summarizing profitability, seasonality, and channel performance


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

Both full-price and discounted-price revenue rise steadily over time, but during November–December the largest spikes come from discounted sales, 
indicating that while full-price demand grows gradually throughout the year, the holiday surge is driven primarily by promotional pricing rather 
than regular-price purchases.

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

**Online** shows the strongest and fastest growth, with revenue and orders rising sharply each year and spiking every Q4.

**Store** is the second-largest contributor, showing reliable seasonal surges.

**Pickup** and **Delivery** remain low-volume channels, they contribute modest revenue with minimal long-term growth and limited seasonal lift.

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

<br><br>
<p align="center">
  <img src="images/Tableau 08b - Profit per Sales Channel .png" width="85%">
</p>

Pickup/Delivery contribute little profit and remain margin-stagnant.
  
<br><br>
<p align="center">
  <img src="images/Tableau 08c - Profit per Customer Segment .png" width="85%">
</p>

Profit is overwhelmingly **Consumer-driven**; SMB/Enterprise play a minimal role .

<br><br>
---

### Business Recommendations

**1. Reduce Over-Dependence on Q4**
- Revenue drops 50–70% every January after holiday peaks.
- Create Q2–Q3 mid-year events to stabilize the reduce seasonality.
- Improve demand forecasting to avoid inventory overstock before Q4.
- Track forecast vs. actual performance using a dedicated FP&A dashboard.

**2. Shift Away From Discount-Heavy Revenue**
- Discounted revenue spikes mainly in Winter and drives volatility.
- Reduce broad seasonal markdowns and move to targeted SKU-level promotions.
- Improve inventory planning to reduce the need for deep discounts.

**3. Expand High-Margin Categories**
- Toys, Beauty, and Clothing deliver the strongest and most reliable profit growth.
- Increase marketing budgets, merchandising depth, and new SKUs in these groups.
- Reassess low-margin areas such as Grocery, Electronics, and Office.

**4. Prioritize Online Sales as the Core Growth Engine**
- Online shows the fastest revenue and profit expansion across all channels.
- Invest in e-commerce UX, retargeting, checkout optimization, and fulfillment.
- Position Pickup and Delivery as support channels rather than growth drivers.

**5. NorthStar Must Acquire More New Customers**
- New customer revenue declines significantly after strong early years.
- Growth is now almost entirely driven by repeat customers, creating long-term risk.
- Launch acquisition-focused campaigns (SEO, paid search, influencer partnerships).
- Add onboarding incentives such as first-purchase bundles or free shipping thresholds.

**6. Strengthen Retention and Loyalty Programs**
- Returning customers are responsible for the majority of total revenue.
- Build lifecycle email flows (welcome, replenishment reminders, win-back messages).
- Add loyalty tiers and personalized product recommendations to increase LTV.





