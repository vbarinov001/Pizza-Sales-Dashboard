# Pizza Sales Dashboard

## 📚 About Data

The pizza sales dataset includes order details, pizza categories, quantities, prices, and timestamps. It provides insights into revenue trends, peak sales hours, and best-selling pizzas.

### Tools

  - SQL - Data Analysis
  - Tableau - Data Visualization

## Exploratory Data Analysis

### KPI's

#### Total Revenue:
```sql
select
  SUM(total_price) as total_revenue)
  FROM pizza_sales;
```
817860.05

#### Average Order Value:
```sql
SELECT
  (SUM(total_price) / COUNT(DISTINCT order_id)) as Avg_order_Value
  FROM pizza_sales
```
38.31

#### Total Pizzas Sold
```sql
SELECT
  SUM(quantity) AS Total_pizzas_sold
  FROM pizza_sales
```
49574

#### Total Orders
```sql
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales
```
21350

#### Average Pizzas Per Order
```sql
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales
```
2.32

### Hourly Trends for Total Pizzas Sold
```sql
SELECT DATEPART(HOUR, order_time) as order_hours, SUM(quantity) as total_pizzas_sold
from pizza_sales
group by DATEPART(HOUR, order_time)
order by DATEPART(HOUR, order_time)
```
![image](https://github.com/user-attachments/assets/00a5085e-434a-45de-9ce9-76fab6ab53ad)

### Weekly Trend for Orders
```sql
SELECT 
    DATEPART(ISO_WEEK, order_date) AS WeekNumber,
    YEAR(order_date) AS Year,
    COUNT(DISTINCT order_id) AS Total_orders
FROM 
    pizza_sales
GROUP BY 
    DATEPART(ISO_WEEK, order_date),
    YEAR(order_date)
ORDER BY 
    Year, WeekNumber;
```
![image](https://github.com/user-attachments/assets/299d0ff6-4c59-4903-8771-5adec76c93bb)
![image](https://github.com/user-attachments/assets/2e9b775b-187e-4d28-8276-649410dd05ae)

### Percentage of Sales by Pizza Category
```sql
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category
```
![image](https://github.com/user-attachments/assets/b4979b60-8132-4f28-9cad-3020f7d69134)

### Percentage of Sales by Pizza Size
```sql
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size
```
![image](https://github.com/user-attachments/assets/00792206-13c1-4c87-9aed-9c97a487a231)

### Total Pizzas Sold by Pizza Category
```sql
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC
```
![image](https://github.com/user-attachments/assets/bd239748-5f07-4880-906c-107edf9dd6b9)

### Top 5 Pizzas by Revenue
```sql
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
```
![image](https://github.com/user-attachments/assets/f8f7f457-38f6-4898-bbd1-4673091a1ef1)

### Bottom 5 Pizzas by Revenue
```sql
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC
```
![image](https://github.com/user-attachments/assets/29172c3c-80cb-45a2-9f90-1dea2a2a010c)

### Top 5 Pizzas by Quantity
```sql
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
```
![image](https://github.com/user-attachments/assets/8eebcb5f-3bd8-4e0a-9906-a070e8f51d16)

### Bottom 5 Pizzas by Quantity
```sql
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
```
![image](https://github.com/user-attachments/assets/33d274ca-2085-4705-bc77-8f34557cdd1a)

### Top 5 Pizzas by Total Orders
```sql
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
```
![image](https://github.com/user-attachments/assets/740a3caf-1ccf-4a69-8756-3a1abd1e97d7)

### Bottom 5 Pizzas by Total Orders
```sql
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
```
![image](https://github.com/user-attachments/assets/d03dcf63-b4e6-4bee-aa65-f61fb75ca6c6)



### 📊 Visualization

Produced a 2-pager dashboard using Tableau
![Screenshot 2025-03-31 154021](https://github.com/user-attachments/assets/c417f3b0-584e-421d-b472-01370cf4f5f5)
![Screenshot 2025-03-31 154029](https://github.com/user-attachments/assets/b3f9ba18-7a88-4372-8284-4b067cfd93ac)

(Dashboard available to download in respective repository)
