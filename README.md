
# Sales Insights - Data Analysis Project

## Problem Statement

The company supplies to hardware to many clients across India. The company has head office at Delhi and lots of regional Offices Throughout India. The Sales Director of the company is facing lots of challenges. The challenges are..
The market is growing dynamically and he is facing challenge tracking sales in different region and having issues with getting insights in dynamically growing market. The Sales Director has different regional managers (i.e. north region, south region etc.). When he needs insights, the regional managers give the insights on phone. The Sales Director is unable to get the real pictures as managers tell everything verbally and try to Sugar quote the sales. When director asks for the numbers then the Managers sends lots of excel files. Now The Sales director is extremely frustrated and unable to figure out the weak points of the business thus unable to find the solution.
The Sales director is more interested in a dashboard where he can have fair idea about all the business insights.
He wants to check data on a daily basis
He also wants to set monthly email reminders of the business sales

## Project Planning (Road Map)

#### Purpose
To unlock sales insights that are not visible before for sales team for decision support & automate them to reduced manual time spent in data gathering.

#### Stakeholders
1. Sales Director
2. Marketing Team
3. Customer Service Team
4. Data & Analytics Team
5. IT

#### End Result
An automated dashboard providing quick & latest sales insights in order to support data driven decision making.

#### Success Criteria
1. Dashboard(s) uncovering sales order insights with latest data available
2. Sales team able to take better decision & prove 10% cost savings of total spend
3. Sales Analysts stop data gathering manually in order to save 20% of their business time and reinvest it value added activity.

## Data Analysis Using SQL

The import of data is done from an already existing MySQL file. This file has to be loaded into MySQL workbench for further data analysis.

Analysis of data by looking into different tables and reflecting garbage values

We can see that garbage value that the table market cantains certain values which are incorrect.

SELECT * FROM sales.market;

And then we can check that transacation table we can see that ceratin negative value in amount which is not possible. and we can see that certain transactions are in USD. Hence, filtration of that is also needed by converting into INR.

SELECT * FROM sales.transactions;

Analysis of different SQL statement on data base

1. To find of all customers records

SELECT * FROM sales.customers;

2. To find total number of customers

SELECT count(*) From sales.customers;

3. To find transactions for Chennai market (market code for chennai is Mark001

SELECT * FROM sales.transactions where market_code='Mark001';

4. To find distrinct product codes that were sold in chennai

SELECT distinct product_code FROM sales.transactions where market_code='Mark001';

5. To find transactions for Chennai market (market code for chennai is Mark002

SELECT * FROM sales.transactions where market_code='Mark002';

6. To find distrinct product codes that were sold in mumbai

SELECT distinct product_code FROM sales.transactions where market_code='Mark002';

7. To find transactions where currency is US dollars

SELECT * from sales.transactions where currency="USD";

8. To find transactions in 2020 join by date table

SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;

9. To find transactions in 2019 join by date table

SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2019;

10. To find total revenue in year 2020,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";

11. To find total revenue in year 2019,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2019 and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";

12. To find total revenue in year 2020, January Month,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");

13. To find total revenue in year 2020, February Month,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="February" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");

14. To find total revenue in year 2019, January Month,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");

15. To find total revenue in year 2019, February Month,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="February" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");

16. To find total revenue in year 2020 in Chennai

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark001";

17. To find total revenue in year 2020 in Mumbai

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark002";
## Data Cleaning and ETL (Extract, Transform, Load)

In this process, we are work on data cleaning and ETL.

#### Step 1:
Connect the MySQL database with the PowerBI desktop.

#### Step 2:
Loading data into the Power BI deskstop. This step load all the tables and created in the data base. This load option will connect with the SQL and pull all the records into power BI environment.

#### Setp 3:
Transform data with the help of Power Query

Perform filtration in market’s table: In the tables perform when we click on the transform data option, we are directed to Power query editor. Power query editor is where we perform out ETL.and then we can perform data transformation i.e. Data Cleaning, Data Wrangling, Data Munging. we need to filter the rows where the values are null and filtering the data and deselecting the blank option.

Perform filtration in Transaction’s table: In the table perform when we check the query in the MySQL to filter some negative values and also 0 values that appears in the table, the desired output is received.and we will perform the similar filtration in PowerBI. we have deselecting the values, don’t want in the table. The result after filtration. the zero values represent some garbage values which is not possible so we need to clean that data.

Convert USD into INR in the transaction’s table: the AtliQ Hardware only works in India so the USD values are not possible. we need to convert those USD values into INR by using some formulas. Add new column - Conditional column - normalized currency where sales amount will be in INR

In power query editore finding the total values having USD as currency.

`=Table.AddColumn(#"Filtered Rows", "norm_sales_amount",each if [currency] = "USD" then [sales_amount]*75 else [sales_amount]`

using this correct formula of the conversion,and converted the USD currency into INR.

In MySQL Workbench find that there are duplicates of USD and INR

 `SELECT count(*) from sales.transactions where sales.transactions.currency="INR\r";` 
 150000 - can't removed as it is large amount

`SELECT count(*) from sales.transactions where sales.transactions.currency="INR";` 
 
279 - we can remove it as it is small record and can be considered as bad data

`SELECT count(*) from sales.transactions where sales.transactions.currency="USD\r";` 

`SELECT count(*) from sales.transactions where sales.transactions.currency="USD";`

 `SELECT * from sales.transactions where sales.transactions.currency='USD\r' or sales.transactions.currency='USD';`

we can see that it is duplicate and for analysis its better to delete anyone of them so lets delete USD and keep USD/r. finally we will keep data with INR/r and USD/r-


## Data Analysis (DAX)

Measures used in all visualization are:

#### Key Measures:

Profit Margin % = DIVIDE([Total Profit Margin],[Revenue],0)

Profit Margin Contribution % = DIVIDE([Total Profit Margin],CALCULATE([Total Profit Margin],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))

Revenue = SUM('sales transactions'[sales_amount])
Revenue Contribution % = DIVIDE([Revenue],CALCULATE([Revenue],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))

Revenue LY= CALCULATE([Revenue],SAMEPERIODLASTYEAR('sales date'[date]))
sales quntity = SUM('sales transactions'[sales_qty])

Total Profit Margin = SUM('Sales transactions'[Profit_Margin])

#### Profit Target:

Profit Target1 = GENERATESERIES(-0.05, 0.15, 0.01)
Profit Target Value = SELECTEDVALUE('Profit Target1'[Profit Target])
Target Diff = [Profit Margin %]-'Profit Target1'[Profit Target Value]
## Tools, Software and Libraries

1. MySQL

2. Microsoft Power BI

3. Power Query Editor

3. DAX Language