## Data Analytics Projects

### Project List
- [Retail Sales Analysis](#retail-sales-analysis)
- [Marketing Campaign Analysis](#marketing-campaign-analysis)
- - #### ICT Analysis (Information Technology)

# Retail Sales Analysis

### Project Overview
Management seeks to gain comprehensive insights into the sales activities of the company from 2016 to 2018. This includes understanding trends and patterns that can inform strategic decisions. Detailed information on revenue generated per region, store, product category, and brand is essential. Additionally, identifying top customers and sales representatives will provide valuable insights into performance and opportunities for targeted improvements.

### Data Acquisition
To address the business problem and meet the stated objectives, I need to acquire and compile the correct dataset.
I will start by acquiring data from the company's sales database. This is an MS SQL Database.
- Data Points Required
  - order_id, customer name, city, state, order_date, total_unit, revenue, product_name, category_name,brand_name, store_name, sale_rep

These data points are dispersed accross various tables, and requires me to write SQL queries to extract the relevant sales, revenue, and customer data from the company’s databases.


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
- Which year performed the best over the period?
- What product category and brand performed and did not perform well?
- Which state outperformed their counterparts?
- Top sales representative per region?

### Data Analytics
This code was used to retrive the data points required to create the dataset, joins on various tables with relevant primary keys on the company's SQL Server Database:

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
### Results 
From an exploratory analysis of the sales data for the period 2016-2018, it appears that 2017 was the best performing year in terms of overall sales and revenue. During this period, mountain bikes emerged as the top product category, reflecting strong consumer demand. Geographically, New York stood out as the highest performing state, contributing significantly to the company's revenue. Among the individual stores, Baldwin Bike distinguished itself as the top performer, leading in sales and customer satisfaction. These insights highlight key areas of success and provide an exploratory view of the current dataset.

### Data Visualization
![Executive Dashboard](https://github.com/Sivacollindarmen/data_analytics/assets/54360140/d7616190-7ad4-48e0-bd21-95565ebac63f)

### Recommendations
Given the insights from the data analysis, here are some solid recommendations to capitalize on the strengths identified and address any potential gaps:

Leverage 2017 Best Practices:
   - Identify and Analyse Success Factors: Investigate what specific strategies, promotions, or market conditions contributed to the outstanding performance in 2017. Replicate these successful tactics in future planning and operations.
   - Sustain Momentum: Focus on maintaining the high standards and effective practices that led to the success in 2017, ensuring consistency in performance.
     
Expand and Promote the Mountain Bike Category:
   - Increase Inventory: Ensure adequate stock levels to meet the high demand for mountain bikes. Consider diversifying the product range within this category to include different models and price points.
   - Marketing Campaigns: Launch targeted marketing campaigns highlighting the popularity and benefits of mountain bikes. Use customer testimonials and success stories to attract new buyers.
   - Partnerships and Sponsorships: Partner with outdoor sports events and sponsorships to boost the visibility of mountain bikes and reach a wider audience.
     
Enhance Presence in New York:
   - Optimize Store Operations: Focus on optimizing operations in New York stores to sustain their top performance. This includes efficient inventory management, superior customer service, and localized marketing efforts.
   - Market Penetration: Explore opportunities for opening new stores or expanding existing ones in New York to capitalize on the strong market presence and high demand.
     
Strengthen Baldwin Bike Store Operations:
   - Recognize and Reward Performance: Acknowledge the achievements of the Baldwin Bike store and its staff. Implement reward programs to motivate continued excellence.
   - Best Practices Implementation: Identify the strategies and practices that have made Baldwin Bike successful and replicate these across other stores. This could include staff 
     training, customer engagement practices, and inventory management.
   - Customer Engagement: Use Baldwin Bike as a model for exceptional customer engagement. Gather customer feedback and use it to continuously improve the shopping experience.
     
Invest in Data-Driven Decision Making:
   - Advanced Analytics: Use advanced analytics to delve deeper into sales patterns, customer preferences, and regional performance. This will provide actionable insights for 
     more informed decision-making.
   - Regular Reporting: Implement a regular reporting mechanism to monitor key performance indicators (KPIs) such as sales trends, product performance, and regional sales on an ongoing basis.
     
Expand Top Performing Regions and Categories:
   - Regional Expansion: Identify other regions with similar characteristics to New York and explore opportunities for expansion.
   - Product Diversification: While focusing on mountain bikes, also explore other categories that showed promise. Introduce complementary products to increase cross-selling opportunities.


# Marketing Campaign Analysis

## Table of contents

### Objective
- What is the key pain point?
  
The Head of Marketing wants to find out who the top YouTubers are in 2024 to decide on which YouTubers would be best to run marketing campaigns throughout the rest of the year.

- What is the ideal solution?
  
To create a dashboard that provides insights into the top UK YouTubers in 2024 that includes their

- subscriber count
- total views
- total videos, and
- engagement metrics
  
This will help the marketing team make informed decisions about which YouTubers to collaborate with for their marketing campaigns.

### User story
As the Head of Marketing, I want to use a dashboard that analyses YouTube channel data in the UK.
This dashboard should allow me to identify the top performing channels based on metrics like subscriber base and average views.

With this information, I can make more informed decisions about which Youtubers are right to collaborate with, and therefore maximize how effective each marketing campaign is.

### Data source

- What data is needed to achieve our objective?
  
We need data on the top UK YouTubers in 2024 that includes their

- channel names
- total subscribers
- total views
- total videos uploaded

- Where is the data coming from?The data is sourced from Kaggle (an Excel extract), see here to find it.

### Stages
- Design
- Developement
- Testing
- Analysis
  
### Design

#### Dashboard components required

- What should the dashboard contain based on the requirements provided?
  
To understand what it should contain, we need to figure out what questions we need the dashboard to answer:

1.Who are the top 10 YouTubers with the most subscribers?
2.Which 3 channels have uploaded the most videos?
3.Which 3 channels have the most views?
4.Which 3 channels have the highest average views per video?
5.Which 3 channels have the highest views per subscriber ratio?
6.Which 3 channels have the highest subscriber engagement rate per video uploaded?

For now, these are some of the questions we need to answer, this may change as we progress down our analysis.

### Dashboard mockup

- What should it look like?
- 
Some of the data visuals that may be appropriate in answering our questions include:

1.Table
2.Treemap
3.Scorecards
4.Horizontal bar chart

