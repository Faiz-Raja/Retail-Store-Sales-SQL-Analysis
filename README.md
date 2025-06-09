# Retail-Store-Sales-SQL-Analysis
This project is a comprehensive Sales Analysis conducted using MySQL, leveraging a dataset sourced from Kaggle. The objective is to perform SQL queries and operations to extract valuable business insights, analyze sales performance trends, and facilitate data-driven decision-making for retail store optimization.
## Key Focus Areas:
• Executing aggregate queries to evaluate total sales, product categories, and seasonal trends.

• Using JOIN operations to correlate sales with customer behavior, store locations, and promotions.

• Applying GROUP BY functions to break down sales by time periods, outlets, and product types.

• Identifying high-performing items and outlets to enhance business strategy.

By leveraging SQL techniques, this analysis helps retailers make informed decisions to improve revenue, enhance inventory management, and optimize marketing efforts.

---
## Questions:
1. What are the details of all transactions made on November 5, 2022?
2. Which transactions involved ‘Clothing’ products where the quantity sold was 4 or more in November 2022?
3. Calculate total sales for each category
4. What is the average age of customers who purchased items from the Beauty category?
5. Which transactions had total sales greater than 1000?
6. How many transactions were made by each gender across different product categories?
7. What is the average sale of each month, and which was the best-selling month in each year?
8. Who are the top 5 customers based on total sales?
9. How many unique customers purchased items from each category?
10. Categorize the transactions into Morning (≤12), Afternoon (12-17), and Evening (>17) shifts?

---
**1. What are the details of all transactions made on November 5, 2022?**

**SQL Query Performed:**

SELECT *

FROM

    retail_sales
    
WHERE

    sale_date = '2022-11-05'

**✅ Insight:** A total of 11 transactions occurred on this specific day across diverse categories like Electronics, Beauty, and Clothing.

**💡 Recommendation:** Peak shopping activity around late afternoon to night (14:00–22:00) suggests ideal promotion windows. Consider time-targeted offers for similar dates in future.

---
**2. Which transactions involved ‘Clothing’ products where the quantity sold was 4 or more in November 2022?**

**SQL Query Performed:**

SELECT *

FROM

    retail_sales
    
WHERE

    category = 'Clothing' AND quantiy >= 4 AND DATE_FORMAT(sale_date, '%b-%y') = 'Nov-22';

**✅ Insight:** There were 17 high-volume clothing transactions (≥ 4 units), spanning various price points and age groups.

**💡 Recommendation:** Bulk purchases may reflect festive buying behavior or discounts. Consider offering volume-based discounts in future sales events to drive similar behavior.

---

**3. Calculate total sales for each category**

**SQL Query Performed:**

SELECT

    category, SUM(total_sale) AS Net_Sales, COUNT(*) AS Total_Orders
    
FROM

    retail_sales
    
GROUP BY 

    category;

| category | Net_Sales | Total_Orders |
| -------- | --------- | ------------ |
| Beauty | 286790 | 611 |
| Clothing | 309995 | 698 |
| Electronics | 311445 | 678 |

**✅ Insight:** Sales are fairly balanced across categories, with Electronics leading slightly in revenue but Clothing having the most orders.

**💡 Recommendation:** All three categories perform well—focus on stock availability and targeted campaigns across all to maintain balance.

---
**4. What is the average age of customers who purchased items from the Beauty category?**

**SQL Query Performed:**

SELECT

    category, ROUND(AVG(age), 2) AS Average_Age, COUNT(*) AS Total_customers
FROM

    retail_sales
    
WHERE

    category = 'Beauty';

| category | Average_Age | Total_Customers |
| -------- | --------- | ------------ |
| Beauty | 40.42 | 611 |

**✅ Insight:** The average customer age for Beauty products is around 40 years, indicating a mature customer base.

**💡 Recommendation:** Consider marketing and product positioning that appeals to this age group—emphasize quality, anti-aging, or premium branding.

---

**5. Which transactions had total sales greater than 1000?**

**SQL Query Performed:**

SELECT

    total_sale, COUNT(total_sale)
    
FROM

    retail_sales
    
WHERE

    total_sale >= 1000
    
GROUP BY 

    total_sale;

| category | Net_Sales |
| -------- | --------- |
|1000|96
|1500|100|
|2000|98|
|1200|108|

**✅ Insight:** A significant number of high-ticket transactions indicate strong premium segment engagement.

**💡 Recommendation:** Promote loyalty rewards or exclusive deals for high-spending customers to increase retention and repeat sales.

---
**6. How many transactions were made by each gender across different product categories?**

**SQL Query Performed:**

SELECT 

    category, gender, COUNT(transactions_id) AS Total_Orders
    
FROM

    retail_sales
    
GROUP BY 

    gender , category
    
ORDER BY

    category;

| category | Male | Female |
| -------- | ---- | ------ |
| Beauty | 281 | 330 |
| Clothing | 351 | 347 |
| Electronics | 343 | 335 |

**✅ Insight:** Purchase distribution is nearly equal between genders across all categories, with slight category preferences (e.g., more females in Beauty, more males in Electronics).

**💡 Recommendation:** Create gender-personalized promotions within each category to optimize targeting (e.g., skincare for females, gadgets for males).

---
**7. What is the average sale of each month, and which was the best-selling month in each year?**

**SQL Query Performed:**

SELECT

    year, month, Average_Sale
    
FROM

    (select year(sale_date) as year, month(sale_date) as month, avg(total_sale) as Average_Sale, rank() over(partition by year(sale_date) order by avg(total_sale)desc) as rn

FROM

    retail_sales
    
GROUP BY

    year(sale_date), month(sale_date) ) as t1
    
WHERE

    rn = 1;

| year | month | Average_Sale |
| ---- | ------| ------------ |
|2022| 7 | 541.34 |
|2023| 2 | 535.53 |

**✅ Insight:** Sales peaked in mid-year (Jul 2022) and early-year (Feb 2023), possibly due to seasonal campaigns or new launches.

**💡 Recommendation:** Plan marketing campaigns and inventory restocks around these high-performing months to capitalize on sales momentum.

---
**8. Who are the top 5 customers based on total sales?**

**SQL Query Performed:**

SELECT

    customer_id, SUM(total_sale) AS Total_Sales
    
FROM

    retail_sales
    
GROUP BY

    customer_id
    
ORDER BY

    Total_Sales DESC LIMIT 5;
    
| customer_id | Total_Sales|
| ----------- | ---------- |
| 3 | 38440 |
| 1 | 30750 |
| 5 | 30405 |
| 2 | 25295 |
| 4 | 23580 |

**✅ Insight:** A few high-value customers contribute significantly to revenue.

**💡 Recommendation:** Consider a VIP or loyalty program to retain and further engage these top spenders.

---
**9. How many unique customers purchased items from each category?**

**SQL Query Performed:**

SELECT 

    category, COUNT(DISTINCT customer_id) AS customers
    
FROM

    retail_sales
    
GROUP BY

    category
    
ORDER BY

    customers DESC;

| category | customers |
| -------- | --------- |
| Clothing | 149 |
| Electronics | 144 |
| Beauty | 141 |

**✅ Insight:** Customer reach is evenly spread across categories, showing broad appeal in the product mix.

**💡 Recommendation:** Maintain variety in product offerings and use cross-category promotions to increase customer overlap.

---
**10. Categorize the transactions into Morning (≤12), Afternoon (12-17), and Evening (>17) shifts?**

**SQL Query Performed:**

WITH

    hourly_sale as
    
	(select *,
	case when hour(sale_time) < 12 then 'Morning'
	when hour(sale_time) between 12 and 17 then 'Afternoon'
	else 'Evening'
	end as shift
	from retail_sales)
	select shift, count(transactions_id) as Total_Orders
	from hourly_sale
 
GROUP BY
    
    shift;

| shift | Total_Orders |
| -------- | --------- |
| Evening | 1062 |
| Morning | 548 |
| Afternoon | 377 |

**✅ Insight:** Evenings dominate sales volume, suggesting it’s the prime shopping window.

**💡 Recommendation:** Align marketing, staffing, and online push notifications with peak evening hours for better sales conversion.

---
**Conclusion (Key-Insights):** This retail sales analysis provides a clear overview of customer behavior, category performance, and sales patterns across time. Clothing emerged as the most purchased category, while Electronics contributed the highest to revenue. Gender preferences are subtle but present, offering room for targeted marketing. Peak sales occur during evening hours, and certain months show stronger performance, indicating seasonal influence. High-value customers and consistent category engagement highlight opportunities for loyalty programs and personalized offers. These insights can guide strategic decisions in marketing, inventory management, and customer engagement to drive growth and optimize sales performance.
