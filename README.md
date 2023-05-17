# PIZZA SALES ANALYSIS
----------------------------------

![](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/Pizza%20Header.jpg)
---------
### Introduction:
_Things are going OK at Plato's, but there's room for improvement. Plato's Pizza have been collecting transactional data for the past year, but haven't been able to put it to good use. As a Data Analyst, Plato's Pizza needs me to analyze the data and put together a report to help them find opportunities to drive more sales and work more efficiently._

### Dataset:

The dataset was downloaded from [Maven](https://www.mavenanalytics.io/blog/maven-pizza-challenge) Analytics website.
### About the dataset
1. This dataset contains 4 tables in CSV format
2. The Orders table contains the date & time that all table orders were placed
3. The Order Details table contains the different pizzas served with each order in the Orders table, and their quantities
4. The Pizzas table contains the size and price for each distinct pizza in the Order Details table, as well as its broader pizza type
5. The Pizza Types table contains details on the pizza types in the Pizzas table, including their name as it appears on the menu, the category it falls under, and its list of ingredients.

### Here are some questions that we'd like to be able to answer:
1. What days and times do we tend to be busiest?
2. How many pizzas are we making during peak periods?
3. What are our best and worst selling pizzas?
4. What's our average order value?
5. How well are we utilizing our seating capacity? (we have 15 tables and 60 seats).

### **Tool Used:** Power BI

### Approach to Analysis
### 1. Extraction, Transformation and Loading (ETL)
I checked through the datasets to check for errors
I checked the data dictionary to fully understand the data sets
I loaded the datasets into POWER BI
I then loaded the data in Power Query

### _While in Power Query…_
I checked and changed the incorrect data types
The **pizza_types** sheet had unpromoted headers, so I used the "Use First Row As Header" function to promote the headers.

|                           Unpromoted Headers                            |         Promoted headers (Used first rows as headers)     |
| ----------------------------------------------------------------------- | --------------------------------------------------------- |
|![](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/Use%20First%20Row%20As%20Header.png) | ![](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/Use%20first%20Row%20as%20Header%20Correct.png)                                                          |
 
I also used the **DATE FUNCTION** in Power Query to extract the date column into **"day", "month", "quarter", and "year"** for better analysis.

|                             Previous Date                               |                       New Extracted Date                  |
| ----------------------------------------------------------------------- | --------------------------------------------------------- |
|![](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/Previous%20Date%20With%20Functions.png) | ![](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/New%20Extracted%20Date.png)                                                          |

I then click "Close & Apply" to exit Power Query and Save my transformations.

### 2. Data Modelling
I created a modelling table to fully represent the facts table, dimensions table, primary keys and foreign keys in the dataset.

![Data Modelling Table](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/Data%20Modelling%20Table.png)

I then applied the table contents to create a model in **Power BI**

![](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/Data%20Modelling.png)

### 3. Data Analysis Expression (DAX)
- I created my Measures Table by clicking on "Enter Data" on the home ribbon.
- I created a new measure **"Total Orders"** using; Total Order = COUNTA(orders[order_id])
- The "order_details" table does not contain a column for prize of pizzas and we need the prize column to be in the same table with the order details in order to calculate the total revenue; To do this, I created a new column to bring the price table to the "order_details" table, Using; Price = RELATED(pizzas[price]).
- I then created another column to calculate the price for each order using; Total Price = order_details[quantity] * order_details[Price].
- I created a new measure **"Total Revenue"** by summing up the "Total Price" Column, Using; Total Revenue = SUM(order_details[Total Price])
- I created a measure **"Average Order revenue"** Using; Average Order Value = [Total Revenue] / [Total Order].
- I created a measure **"Order per Quarter"** Using; Order per Quarter = [Total Order] / DISTINCTCOUNT(orders[Name of Quarter]).

### DASHBOARD: 
I created an interactive and dynamic dashboard to help Plato's Pizza understand business transactions and to drive more sales and work efficiently. 
For easy view and understanding, I created three dashboards; **Overview dashboard, Orders Dashboard** and **Revenue Dashboard.**

![Overview Dashboard](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/Pizza%20Sales%20(Page%201).jpg)

![Orders Dashboard](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/Pizza%20Sales%20(Page%202).jpg)

![Revenue Dashboard](https://github.com/BiolaBolade/Pizza-Sales-Analysis/blob/main/pizza_sales/Pizza%20Sales%20(Page%203).jpg)

### Interact with the dashboard [here](https://app.powerbi.com/view?r=eyJrIjoiYTk3MjdhYjktM2I5NC00YTlhLTg4YzUtZjk4MDUzNzUxN2Y0IiwidCI6IjM4ZmY0NTNhLWEwZjktNGZkMy1iNTIyLTUwZWNiMmVjNDAzZiJ9)

### INSIGHTS:
- The total number of orders received was 21,350. The Classic Deluxe Pizza was the Best Selling Pizza by Orders, with total orders of 2329. Of course, The Brie Carre Pizza was the Worst Selling Pizza by Orders, generating the lowest number of orders (480). We had the highest order in July (1935) while the lowest order we received was in October (1646).
- There is a positive correlation between orders and revenue i.e., as the number of orders increase, the revenue also increases and vice-versa.
- Analysis revealed that we have peak hours between 12:00PM with 2520 orders and 1:00PM with 2455 orders. This is usually the lunch break hour for most organizations. We hit a top order of 3538 and Fridays and 3239 on Thursdays. This reveals that Fridays are our most busy days.
- The total revenue generated was $817.86K. The Thai Chicken Pizza was the Best Selling Pizza by Revenue, generating $43.43K. The Brie Carre Pizza was the Worst Selling Pizza by Revenue, generating $11.59K. We made the Highest Revenue of $208.37K in Quarter 2. We accrued a total revenue of $72.5K in July, making July the month we had our highest revenue, while we generated the lowest revenue ($64K) in October.
- We have 15 tables and 60 seats which means that each table has 4 seats on average. From analysis, tables are well-utilized every hour and there are enough tables for every customer but during a period of high peak hours, the seats and tables were insufficient on very few occasions. 

### RECOMMENDATIONS:
1. The Brie Carre Pizza is the worst selling pizza. A survey should be carried out to know what customers think about this pizza. By doing this, we can solve the issues behind The Brie Carre Pizza being the worst selling pizza. Through rebranding, changing recipes or any other means. We should increase the production rate of the best selling pizza to generate more revenue from it.
2. There should be an improvement in our delivery channels to increase the delivery rate during days and hours of high orders. We should also implement online ordering channel, this will make people who can't leave their comfort zone make seamless and have thier pizza delivered in no time.
3. It is recommended to offer a promo on days when low sales and revenue are generated. Likewise, a seasonal promo should be offered during Valentine, mother's day, Christmas, Eid, etc.
4. We should get a few more tables and seats. Also, it will be nice to have tables with two seats only, for couples who wants to spend time together.
--------------------------------
_Thank you for reading_ 🙏
