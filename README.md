# nyc_retail_sql_tableau_analytics
A 5-year retail analytics case study using PostgreSQL + Tableau, modeling revenue, customers, profitability, and seasonality for a fictitious NYC-based omnichannel retailer (NorthStar).


# NorthStar NYC Retail — 5-Year Customer & Sales Analytics (PostgreSQL and Tableau visualization)

---

## 1. Project Overview

This project simulates a large omnichannel retailer serving the New York City metropolitan area between 2020–2024.  
Think of a NYC-focused version of **Target, Walmart, or Costco**.

The goal is to demonstrate real-world SQL analytics workflows, including:

- Revenue & transaction trend analysis  
- Customer behavior and lifecycle analytics  
- Month-over-month (MoM) growth  
- Cohort & retention analysis  
- Customer Lifetime Value (LTV) modeling  
- Category & department performance  
- Seasonality and multicultural holiday effects  
- Window functions (LAG, LEAD, rolling averages)  
- Fact–dimension modeling with a star-schema approach  

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
