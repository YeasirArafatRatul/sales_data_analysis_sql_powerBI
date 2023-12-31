USE sales;
/* How many data are in this table?*/
SELECT COUNT(*) AS number_of_transactions FROM sales.transactions;

/* Find the total amount sold to each customer in lifetime */
SELECT sales.customers.customer_code, SUM(sales.transactions.sales_amount) AS total_amount_sold
FROM sales.transactions
JOIN sales.customers
ON sales.transactions.customer_code = customers.customer_code
GROUP BY customers.customer_code;

/* Sort the list of customers by the total amount bought by each customer */
SELECT sales.customers.customer_code, SUM(sales.transactions.sales_amount) AS total_amount_sold
FROM sales.transactions
JOIN sales.customers
ON sales.transactions.customer_code = customers.customer_code
GROUP BY customers.customer_code
ORDER BY total_amount_sold DESC;

/* Find top 5 customers who bought highest amount */
SELECT sales.customers.customer_code, SUM(sales.transactions.sales_amount) AS total_amount_sold
FROM sales.transactions
JOIN sales.customers
ON sales.transactions.customer_code = customers.customer_code
GROUP BY customers.customer_code
ORDER BY total_amount_sold DESC
LIMIT 5;

/* Let's find transactions only from mumbai */
SELECT * FROM sales.transactions WHERE market_code = "Mark002";


/* Let's find how much sold in which city individually */
SELECT markets_name, SUM(sales.transactions.sales_amount) AS total_sold
FROM sales.transactions
JOIN sales.markets
ON transactions.market_code = markets.markets_code
GROUP BY market_code;