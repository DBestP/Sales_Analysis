# Sales Analysis

![](Sales_Analysis.jpg)

***
### **Tools used: MSSQL**

***
### Introduction:
This dataset is detailed sales data, with customer information, sales details, product details, and order transactional records like business location, etc.  By analyzing this data, we aim to uncover trends, patterns, and actionable insights that can enhance strategic decisions for the continued success and improvement of the Superstore.

***
 ### Problem Statement
I want to determine the sales performance, identify the key factors influencing the sales performance and propose actionable strategies to optimize revenue, reduce costs, and enhance customer satisfaction within the Superstore.

***
# Project Scope

## 1. Sales and Profit Analysis
- Calculate the total sales amount for each category.
- Determine the total profit for each sub-category.
- Explore average profit margins for individual products.

## 2. Discount Insights
- Compute average discounts for different customer segments.
- Identify the region with the highest average discount.

## 3. Geographical Trends
- Determine the country with the highest total sales.
- Analyse sales by state and city (e.g., highest average sales per order).

## 4. Yearly and Monthly Insights
- Summarize total sales by year and month.
- Investigate monthly sales trends.

## 5. Product-Level Metrics
- Quantify the quantity sold for each product.

## 6. Customer-Centric Metrics
- Find the total sales amount for each customer.

## 7. Shipping Modes and Profitability
- Explore total sales by ship mode.
- Assess overall profit by state.

## 8. Top-Performing Product
- Identify the product with the highest total sales amount.

## 9. Order Profitability
- Compute average order profit for each category.

***
### SQL Analysis
  1.	**Sales and Profit Analysis:**
- Calculate total sales amount for each category.
```Sql
-- Calculate total sales amount for each category.
select category,
Round (sum (sales),2) As Total_Sales
from Superstore
group by category;
-- This query is ment return total sales by category,
-- rounded-up to 2 decimal places.
``` 

- Determine total profit for each sub-category.
```SQL
Select 
Sub_Category, Round (sum (Profit),2) As Total_Sub_Profit
from Superstore
Group by Sub_Category
Order by Total_sub_Profit;
--This reveals the total profit or loss gotten from each sub_categories
```

- Explore average profit margins for individual products.
```sql
select Product_Name, round (AVG (Profit/Sales)*100,2) As Avg_Profit_Magin
from Superstore
group by Product_Name
order by Avg_Profit_Magin desc;
-- The aim of this question is to determine the percentage gain or 
--loss gotten from each product and perhaps review their business strategies
--particulaly on underperforming products
```

***
2. **Discount Insights:**
-	Compute average discounts for different customer segments.
```sql
Select segment, 
Round (avg(discount),2) As Average_Discount
from Superstore
Group by Segment
order by Average_Discount;
-- This is ment to avearage discount for each segment,
-- in order to evaluate the appropriateness of the discount given for each segment,
-- and the corresponding expected returns (as a result of the discount).
  ```
-	Identify the region with the highest average discount.
```sql
 Select Region, 
 Round (avg (discount),2) Avg_Reg_Discount
 from Superstore
 Group by Region
 Order by Avg_Reg_Discount desc;
 -- This returns regions with the highest average discount
```

***
3.	**Geographical Trends:**
-	Determine the State with the highest total sales.
  ```sql
select top 1 Round (Sum (sales), 2) As Total_Sales,
State 
from Superstore
Group by State
-- This is to return the state with the highest sales
-- But in this case I think the question would have been to know the countries total sals
-- however for the countries total sales is;
```
  
-	Analyse sales by state and city (e.g., highest average sales per order).
  ```sql
 Select Top 1 round (AVG (Sales),2) as Avg_Sales,
 City
 from Superstore
 group by City;
 select * from Superstore
 -- This is to determine the location with the highest avg sales.
```

***
4.	**Yealy, Monthly Insights:**
-	Summarize total sales by year and month.
  
```sql
Select 
Year( order_date) As Year,
Round (Sum (sales),2) as Total_Sale
from Superstore
Group by year (order_date)
Order by Year asc
-- This is supposed to return the total the
--sales from each year, so as to esterblish the with the highest or
--lowest sales and possibly question it for better improvement.
```
-	Investigate monthly sales trends.
```sql
 SELECT
FORMAT(order_date, 'MMMM') AS MonthName,
Round(sum(sales),2) as Total_Sales_per_Month
 from Superstore
 group by  FORMAT(order_date, 'MMMM')
 order by Total_Sales_per_Month;
 -- This returns the sales according to months.
```

***
5.	**Product-Level Metrics:**
-	Quantify quantity sold for each product.
  ```sql
Select distinct Product_Name, 
SUM( Quantity) as Qty_Sold
from Superstore
Group by Product_Name
order by Qty_Sold desc
--the question here is determine the performance of each product
-- thereby making a decision on the product performance.
-- for example, only 1 quantiy of xerox 20 was sold within the years in review.
```

***
6	**Customer-Centric Metrics:**
-	Find total sales amount for each customer.
```sql
 Select distinct (customer_Name), Round (sum(sales),2) as Total_sales
 from superstore
 group by customer_name
 order by Total_sales desc;
```

***
7	**Shipping Modes and Profitability:**
-	Explore total sales by ship mode.
```sql
Select Ship_Mode, Round(SUM(sales),2) as Total_Sales
 from Superstore
 Group by Ship_Mode
 Order by Total_Sales desc
```
-	Assess overall profit by each state.
  ```sql
Select State, Round(sum(profit),2) as Total_Profit
 from Superstore
 Group by State
 order by Total_Profit;
 -- This returns the profit or loss made by each state
```

***
8.	**Top-Performing Product:**
-	Identify the product with the highest total sales amount.
  ```sql
 Select  top 1 Round(SUM(sales),2) as Highest_sales,
 Product_Name
 from Superstore
 group by Product_Name
 order by Highest_sales desc
 -- Here is to determine the product that made the highest sales.
```

***
9.**Order Profitability:**
-	Compute average order profit for each category.
```sql
 SELECT
  CATEGORY,
 ROUND(AVG (PROFIT),2) AS AVG_CATEGORY_PROFT
 FROM SUPERSTORE
 GROUP BY CATEGORY
 --THIS RETURNS AVERAGE PROFIT MADE FROM EACH OF THE PRODUCT CATEGORIES
```

***
# Sales Strategy Recommendations

1. **Strategic Resource Allocation**
   - Prioritize inventory and marketing efforts for high-performing categories.
   - Allocate additional resources to support growth in these key areas.
   - Invest in categories that significantly contribute to overall sales.

2. **Cost and Pricing Optimization**
   - Identify and address high-cost areas to improve margins.
   - Implement cost-saving practices across the supply chain.
   - Consider price adjustments to enhance profitability.

3. **Tailored Discount Strategies**
   - Customize discounts for different customer groups to boost satisfaction and loyalty.
   - Ensure discounts are balanced to maintain profitability while attracting customers.

4. **Geographical and Seasonal Focus**
   - Focus marketing and inventory efforts on high-sales regions.
   - Develop localized marketing campaigns to cater to regional preferences and needs.
   - Align business strategies with observed seasonal sales trends.

5. **Product and Customer Management**
   - Promote high-demand products through increased marketing efforts.
   - Evaluate and consider discontinuing low-selling products.
   - Enhance loyalty programs and personalized interactions for high-value customers.
   - Optimize logistics and delivery options to improve customer satisfaction and cost efficiency.

***
Thank you for taking the time to explore this project. Your interest and attention are genuinely appreciated. If you have any contributions or suggestions, I welcome the opportunity to connect and discuss any ideas you may have. Feel free to reach out to me on [LinkedIn](https://www.linkedin.com/in/bestman-peter/). I would love to engage in a conversation and hear your thoughts. Looking forward to connecting!

