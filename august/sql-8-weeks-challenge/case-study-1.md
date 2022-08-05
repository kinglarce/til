# Case Study 1

{% embed url="https://8weeksqlchallenge.com/case-study-1/" %}

{% embed url="https://dbdiagram.io/d/608d07e4b29a09603d12edbd/?utm_medium=bottom_open&utm_source=dbdiagram_embed" %}

Each of the following case study questions can be answered using a single SQL statement:

What is the total amount each customer spent at the restaurant?

```sql
SELECT 
  sales.customer_id, 
  SUM(price) 
FROM 
  dannys_diner.sales as sales 
  JOIN dannys_diner.menu as menu ON menu.product_id = sales.product_id 
GROUP BY 
  sales.customer_id;
```

How many days has each customer visited the restaurant?

```sql
SELECT 
  sales.customer_id, 
  COUNT(
    DISTINCT(sales.order_date)
  ) as visit_count
FROM 
  dannys_diner.sales as sales 
GROUP BY 
  sales.customer_id;
```

What was the first item from the menu purchased by each customer?

```sql
// Some code
```

What is the most purchased item on the menu and how many times was it purchased by all customers?



Which item was the most popular for each customer?



Which item was purchased first by the customer after they became a member?



Which item was purchased just before the customer became a member?



What is the total items and amount spent for each member before they became a member?



If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?



In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?

