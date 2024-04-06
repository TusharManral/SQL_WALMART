**SQL PROJECT**

**Walmart Sales Data Analysis**
About This project aims to explore the Walmart Sales data to understand top performing branches and products, sales trend of of different products, customer behaviour. The aims is to study how sales strategies can be improved and optimized. The dataset was obtained from the Kaggle Walmart Sales Forecasting Competition.

"In this recruiting competition, job-seekers are provided with historical sales data for 45 Walmart stores located in different regions. Each store contains many departments, and participants must project the sales for each department in each store. To add to the challenge, selected holiday markdown events are included in the dataset. These markdowns are known to affect sales, but it is challenging to predict which departments are affected and the extent of the impact." source

**Purposes Of The Project**
The major aim of thie project is to gain insight into the sales data of Walmart to understand the different factors that affect sales of the different branches.

**About Data**
The dataset was obtained from the Kaggle Walmart Sales Forecasting Competition. This dataset contains sales transactions from a three different branches of Walmart, respectively located in Mandalay, Yangon and Naypyitaw. The data contains 17 columns and 1000 rows:

Column	Description	Data Type
invoice_id	Invoice of the sales made	VARCHAR(30)
branch	Branch at which sales were made	VARCHAR(5)
city	The location of the branch	VARCHAR(30)
customer_type	The type of the customer	VARCHAR(30)
gender	Gender of the customer making purchase	VARCHAR(10)
product_line	Product line of the product solf	VARCHAR(100)
unit_price	The price of each product	DECIMAL(10, 2)
quantity	The amount of the product sold	INT
VAT	The amount of tax on the purchase	FLOAT(6, 4)
total	The total cost of the purchase	DECIMAL(10, 2)
date	The date on which the purchase was made	DATE
time	The time at which the purchase was made	TIMESTAMP
payment_method	The total amount paid	DECIMAL(10, 2)
cogs	Cost Of Goods sold	DECIMAL(10, 2)
gross_margin_percentage	Gross margin percentage	FLOAT(11, 9)
gross_income	Gross Income	DECIMAL(10, 2)
rating	Rating	FLOAT(2, 1)
Analysis List
Product Analysis
Conduct analysis on the data to understand the different product lines, the products lines performing best and the product lines that need to be improved.

**Sales Analysis**
This analysis aims to answer the question of the sales trends of product. The result of this can help use measure the effectiveness of each sales strategy the business applies and what modificatoins are needed to gain more sales.

**Customer Analysis**
This analysis aims to uncover the different customers segments, purchase trends and the profitability of each customer segment.

**Approach Used**
Data Wrangling: This is the first step where inspection of data is done to make sure NULL values and missing values are detected and data replacement methods are used to replace, missing or NULL values.
**Build a database**
Create table and insert the data.
Select columns with null values in them. There are no null values in our database as in creating the tables, we set NOT NULL for each field, hence null values are filtered out.
**Feature Engineering**: This will help use generate some new columns from existing ones.
Add a new column named time_of_day to give insight of sales in the Morning, Afternoon and Evening. This will help answer the question on which part of the day most sales are made.
Add a new column named day_name that contains the extracted days of the week on which the given transaction took place (Mon, Tue, Wed, Thur, Fri). This will help answer the question on which week of the day each branch is busiest.
Add a new column named month_name that contains the extracted months of the year on which the given transaction took place (Jan, Feb, Mar). Help determine which month of the year has the most sales and profit.
**Exploratory Data Analysis (EDA)**: Exploratory data analysis is done to answer the listed questions and aims of this project.

**Conclusion:**

Business Questions To Answer
Generic Question
How many unique cities does the data have?
In which city is each branch?
Product
How many unique product lines does the data have?
What is the most common payment method?
What is the most selling product line?
What is the total revenue by month?
What month had the largest COGS?
What product line had the largest revenue?
What is the city with the largest revenue?
What product line had the largest VAT?
Fetch each product line and add a column to those product line showing "Good", "Bad". Good if its greater than average sales
Which branch sold more products than average product sold?
What is the most common product line by gender?
What is the average rating of each product line?
Sales
Number of sales made in each time of the day per weekday
Which of the customer types brings the most revenue?
Which city has the largest tax percent/ VAT (Value Added Tax)?
Which customer type pays the most in VAT?
Customer
How many unique customer types does the data have?
How many unique payment methods does the data have?
What is the most common customer type?
Which customer type buys the most?
What is the gender of most of the customers?
What is the gender distribution per branch?
Which time of the day do customers give most ratings?
Which time of the day do customers give most ratings per branch?
Which day fo the week has the best avg ratings?
Which day of the week has the best average ratings per branch?


















SQL PROJECT

create table if not exists	Walmartsalesdatat(
invoice_id VARCHAR(30) Not Null,
branch VARCHAR(30) Not null,
city VARCHAR(30) Not null,
customer_type VARCHAR(30) Not null,
gender VARCHAR(10) Not null,
product_line varchar(100) not null,
unit_price DECIMAL(10, 2) Not null,
quantity INT Not null,
VAT FLOAT(6, 4) Not null,
total DECIMAL(10, 2) Not null,
date DATE Not null,
time TIMESTAMP Not null,
payment_method DECIMAL(10, 2) Not null,
cogs 	DECIMAL(10, 2) Not null,
gross_margin_percentage FLOAT(11, 9) Not null,
gross_income DECIMAL(10, 2) Not null,
rating 	FLOAT(2, 1) Not null,
CONSTRAINT PK_invoice_id PRIMARY KEY (invoice_id));
use Famous_Paintings;

SELECT * FROM Famous_Paintings.walmartsalesdata;

-- 1)Data Wrangling: This is the first step where inspection of data is done to make sure NULL values and missing values are detected 
-- and data replacement methods are used to replace, missing or NULL values.

-- Build a database
-- Create table and insert the data.
-- Select columns with null values in them. There are no null values in our database as in creating the tables, 
-- we set NOT NULL for each field, hence null values are filtered out.

-- 2Feature Engineering: This will help use generate some new columns from existing ones.
-- 1)Add a new column named time_of_day to give insight of sales in the Morning, Afternoon and Evening. 
-- This will help answer the question on which part of the day most sales are made.
-- 2)Add a new column named day_name that contains the extracted days of the week on which the given transaction took 
-- place (Mon, Tue, Wed, Thur, Fri). This will help answer the question on which week of the day each branch is busiest.
-- 3)Add a new column named month_name that contains the extracted months of the year on which the given transaction took 
-- place (Jan, Feb, Mar). Help determine which month of the year has the most sales and profit.

select time,
( case
       when `time` between '00:00:00' and '12:00;00' then 'Morning'
	   when `time` between '12:01:00' and '16:00;00' then 'Afternoon'
       
ELse 'Evening'
END
) as Time_of_date
from walmartsalesdata;

alter table walmartsalesdata add column time_of_date varchar(20);

update walmartsalesdata
set Time_of_date = (case
       when `time` between '00:00:00' and '12:00;00' then 'Morning'
	   when `time` between '12:01:00' and '16:00;00' then 'Afternoon'
ELse 'Evening'
END);

-- DAY NAME;

select dayname(Date) as Day_name from walmartsalesdata;

alter table walmartsalesdata add column Day_name Varchar(10);

update walmartsalesdata
set  Day_name=(dayname(Date));

select * from walmartsalesdata;

-- get column of Month_name
select monthname(date) as month_name from walmartsalesdata;

alter table walmartsalesdata add column month_name varchar(20); 

update walmartsalesdata
set  month_name=(monthname(date));

select * from walmartsalesdata;

-- Generic Question

-- How many unique cities does the data have?
select distinct city
from walmartsalesdata;


-- In which city is each branch?

select city, count(Branch) from walmartsalesdata
group by city;

-- Product
-- How many unique product lines does the data have?

select distinct(`Product Line`) from walmartsalesdata;

-- What is the most common payment method?

select payment, count(payment) from walmartsalesdata
group by payment
order by count(payment) Desc;
-- Ewallet is the most used payment method.

-- What is the most selling product line?

select `Product line`, count(*) from walmartsalesdata
group by `Product line`
order by count(*) DESC;

-- What is the total revenue by month?

select month_name, sum(total) from walmartsalesdata
group by month_name Desc;

-- What month had the largest COGS?

select month_name,sum(cogs) from walmartsalesdata
group by month_name
order by month_name Desc;

-- What product line had the largest revenue?

select `product line`,sum(total) as revenue from walmartsalesdata
group by `product line`
order by revenue Desc;

-- What is the city with the largest revenue?

select city,sum(total) as revenue from walmartsalesdata
group by city
order by revenue Desc;

-- What product line had the largest VAT?

select `product line`, sum(`Tax 5%`) from walmartsalesdata
group by `product line`
order by sum(`Tax 5%`) Desc;


-- Fetch each product line and add a column to those product line showing "Good", "Bad". Good if its greater than average sales

select `Product line`, sum(total),
case 
    when sum(total)>(select avg(total) from walmartsalesdata) then 'Good'
    when sum(total)<(select avg(total) from walmartsalesdata) then 'Bad'
END
from walmartsalesdata
group by `Product line`;


-- Which branch sold more products than average product sold?

select `product line`, sum(total)  as revenue
from walmartsalesdata
group by `product line`
having revenue > (select avg(total) from walmartsalesdata);

-- What is the most common product line by gender?

select `Product line`, count(Gender) as number, gender from walmartsalesdata
group by `Product line`, gender
order by number Desc;

-- What is the average rating of each product line?

select `product line`,avg(Rating) from walmartsalesdata
group by `product line`
order by avg(Rating) Desc;

-- Sales
-- Number of sales made in each time of the day per weekday

select day_name, time_of_date, 
sum(total)  as sales
from walmartsalesdata
where day_name in ('sunday','Monday','Tuesday','Wednesday', 'Thrusday','Friday','saturday')
group by time_of_date, day_name
order by sales ;

-- Which of the customer types brings the most revenue?

select `customer type`, sum(total) from walmartsalesdata
group by `customer type`
order by sum(total);

-- Which city has the largest tax percent/ VAT (Value Added Tax)?

select city, max(`Tax 5%`) from walmartsalesdata
group by city
limit 1;

-- Which customer type pays the most in VAT?

select `customer type`, max(`Tax 5%`) from walmartsalesdata
group by `customer type`;


-- ------------------------------------------ CUSTOMER-----------------------------------------
-- How many unique payment methods does the data have?

select distinct(payment) from walmartsalesdata;

-- What is the most common customer type?

select `Customer type`, count(*) from walmartsalesdata
group by `Customer type`;

-- Which customer type buys the most?

select `customer type`, (`Unit price`* Quantity) as Spend
from walmartsalesdata
group by `customer type`
order by spend DEsc;

-- What is the gender of most of the customers?

select Gender, count(*) from walmartsalesdata
group by Gender;

-- What is the gender distribution per branch?

select branch, gender, count(gender) from walmartsalesdata
group by branch, gender;

-- Which time of the day do customers give most ratings?

select time_of_date, rating from walmartsalesdata
group by time_of_date
order by rating Desc;

-- Which time of the day do customers give most ratings per branch?

select branch,time_of_date, rating from walmartsalesdata
group by branch,time_of_date
order by rating Desc, branch Asc;


-- Which day of the week has the best avg ratings?

select day_name, avg(Rating) from walmartsalesdata
group by day_name
order by avg(Rating) Desc;

-- Which day of the week has the best average ratings per branch?

select branch,day_name,avg(rating) from walmartsalesdata
group by branch, day_name
order by avg(rating) Desc, Branch;
