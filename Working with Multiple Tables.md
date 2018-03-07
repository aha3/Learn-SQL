# Working with Multiple Tables
In this lesson, we'll learn the SQL commands that will help us work with data that is stored in multiple tables.

## Introduction

In order to efficiently store data, we often spread related information across multiple tables.
For instance, imagine that we're running a magazine company where users can have different types of subscriptions to different products. Different subscriptions might have many different properties. Each customer would also have lots of associated information.
We could have one table with all of the following information:

•	order_id

•	customer_id

•	customer_first_name

•	customer_last_name

•	customer_address

•	subscription_id

•	subscription_description

•	subscription_length

•	subscription_monthly_price

•	purchase_date

However, a lot of this information would be **repeated**. 
If the same customer has multiple subscriptions, that customer's name and address will be reported multiple times. 
If the same subscription type is ordered by multiple customers, then the subscription price and subscription description will be repeated. 
This will **make our table big and unmanageable**.

So instead, we can split our data into three tables:

•	orders would contain just the information necessary to describe what was ordered:

o	order_id

o	customer_id

o	subscription_id

o	purchase_date


•	subscriptions would contain the information to describe each type of subscription:

o	subscription_id

o	subscription_description

o	subscription_monthly_price

o	subscription_length

•	customers would contain the information for each customer:

o	customer_id

o	customer_name

o	customer_address

### Instructions
1.
Examine these tables by pasting the following code into the editor:
```sql
SELECT * FROM orders; 
SELECT * FROM subscriptions; 
SELECT * FROM customers;
```

## Combining Tables Manually

