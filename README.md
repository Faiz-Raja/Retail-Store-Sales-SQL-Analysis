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

