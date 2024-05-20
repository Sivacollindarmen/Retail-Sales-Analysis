# Data Analytics Projects

### Table of Contents
 - [Project List](#project-list)
 - 

### Project List
- [Sales Revenue Analysis](#sales-revenue-analysis)
- #### Financial Analysis (Banking)
- #### ICT Analysis (Information Technology)

# Sales Revenue Analysis

### Project Overview
Management seeks to gain comprehensive insights into the sales activities of the company from 2016 to 2018. This includes understanding trends and patterns that can inform strategic decisions. Detailed information on revenue generated per region, store, product category, and brand is essential. Additionally, identifying top customers and sales representatives will provide valuable insights into performance and opportunities for targeted improvements.

### Data Acquisition
To address the business problem and meet the stated objectives, I need to acquire and compile the correct dataset.
I will start by acquiring data from the company's sales database. This is a MS SQL Database.
- Data Points Required
  - order_id, customer name, city, state, order_date, total_unit, revenue, product_name, category_name,brand_name, store_name, sale_rep

These data points are dispersed accross various tables, and requires me to write SQL queries to extract the relevant sales, revenue, and customer data from the company’s databases.

```Sql
SELECT 
ord.order_id,
CONCAT(cus.first_name,' ', cus.last_name) AS 'customers',
cus.city,
cus.state,
ord.order_date,
SUM(ite.quantity) AS 'total_units',
SUM(ite.quantity * ite.list_price) AS 'revenue',
pro.product_name,
cat.category_name,
sto.store_name,
CONCAT(sta.first_name,' ',sta.last_name) AS 'sales_rep'
FROM sales.orders ord
JOIN sales.customers cus
ON ord.customer_id = cus.customer_id
JOIN sales.order_items ite
ON ord.order_id = ite.order_id
JOIN production.products pro
ON ite.product_id = pro.product_id
JOIN production.categories cat
ON pro.category_id = cat.category_id
JOIN sales.stores sto
ON ord.store_id = sto.store_id
JOIN sales.staffs sta
ON ord.staff_id = sta.staff_id
GROUP BY
ord.order_id,
CONCAT(cus.first_name,' ', cus.last_name),
cus.city,
cus.state,
ord.order_date,
pro.product_name,
cat.category_name,
sto.store_name,
CONCAT(sta.first_name,' ',sta.last_name)
```

### Tools
- Excel
- SQL Server
- Power BI
- Tableau

### Data Preparation 
- In the initial preparation phase I performed the follwing tasks:
  1. Data loading and inspection
  2. Handling missing values
  3. Normalization, cleaning and formatting

### Exploratory Data Analysis 

### Data Analytics

### Recommendation 

### Limitations 

### References 
