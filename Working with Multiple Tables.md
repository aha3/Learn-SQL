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

Let's return to our magazine company. Suppose we have the three tables described in the previous exercise. 
The tables are shown in the far right panel.
If we just look at the orders table, we can't really tell what's happened in each order. However, if we refer to the other tables, we can get a more complete picture.

Let's examine the order with an order_id of 2. It was purchased by customer 2. To find out the customer's name, we look at the customers table and look for the item with a customer_id value of 2. We can see that Customer 2's name is Jane Doe and that she lives at 456 Park Ave.

Doing this kind of matching is called **joining** two Tables.

### Instructions
1.
Using the tables displayed, what is the description of the magazine ordered in order 1?
Type your answer on line 1 of the code editor. Be sure to capitalize it the same as in the table.

## Combining Tables with SQL

Combining tables manually is **time-consuming**. Luckily, SQL gives us an easy sequence for this: it's called a `JOIN`.

If we want to combine orders and customers, we would type:
```sql
SELECT * 
FROM orders 
JOIN customers 
ON orders.customer_id = customers.customer_id
```

Let's break down this command:
1.	The first line **selects all columns** from our combined table. If we only want to select certain columns, we can specify which ones we want.
2.	The second line **specifies the first table** that we want to look in, orders
3.	The third line uses `JOIN` to say that we want to **combine information from orders with customers**.
4.	The fourth line tells us **how to combine the two tables**. We want to match customer_id from orders with customer_id from customers.

Because column names are often repeated across multiple tables we use the syntax `table_name.column_name` **to be sure that our requests for columns are unambiguous**. In our example, we use this syntax in the `ON` statement, but we will also use it in the `SELECT` or any other statement where we refer to column names.

For example, if we only wanted to select the order_id from orders and the customer_name from customers, we could use the following query:
```sql
SELECT orders.order_id, customers.customer_name 
FROM orders 
JOIN customers 
ON orders.customer_id = customers.customer_id
```
### Instructions
1.
Join orders and subscriptions and select all columns. Make sure to join on subscription_id.

```sql
SELECT *
FROM orders
JOIN subscriptions
	ON orders.subscription_id = subscriptions.subscription_id;
  ```
2.
Add a second query after your first one that only selects rows from the join where description is equal to 'Fashion Magazine'.

```sql
SELECT *
FROM orders
JOIN subscriptions
	ON orders.subscription_id = subscriptions.subscription_id
WHERE subscriptions.description = 'Fashion Magazine';
```

## Inner Joins

Let's revisit how we joined `orders` and `customers`. For every possible value of `customer_id` in `orders`, there was a corresponding row of customers with the same `customer_id`.

What if that wasn't true?

For instance, imagine that our `customers` table was out of date, and was missing any information on customer 11. If that customer had an order in `orders`, what would happen when we joined the tables?

When we perform a simple `JOIN` (often called an **inner join**) our result only includes **rows that match our `ON` condition**.

Consider the following GIF, which illustrates an inner join of two tables on `table1.c2 = table2.c2`:

![inner-join](https://user-images.githubusercontent.com/33429899/37095305-cc245ade-2215-11e8-8ac1-b4ed36b4d7e3.gif)

The first and last rows have matching values of `c2`. The middle rows do not match. The final result has all values from the first and last rows **but does not include the non-matching middle row.**
