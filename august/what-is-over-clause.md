---
description: Wednesday, August 11, 2022
---

# What is OVER() Clause

For simplistic terms, if you want to aggregate multiple records such as calculating average or sum for each row, you can use `GROUP BY` , but if you don't want to only aggregate the subset data, you can use the `OVER` clause with `PARTITION BY` which will create a subset group of data.

{% code title="Clause definition" %}
```sql
<function> OVER ([PARTITION BY clause]
                 [ORDER BY clause]
                 [ROWS or RANGE clause])
```
{% endcode %}

Here, I want to know what's the first item purchase by each customer.\
\
**Sales** Table

| customer\_id | order\_date | product\_id |
| ------------ | ----------- | ----------- |
| A            | 2021-01-01  | 1           |
| A            | 2021-01-01  | 2           |
| A            | 2021-01-07  | 2           |
| A            | 2021-01-10  | 3           |
| A            | 2021-01-11  | 3           |
| A            | 2021-01-11  | 3           |
| B            | 2021-01-01  | 2           |
| B            | 2021-01-02  | 2           |
| B            | 2021-01-04  | 1           |
| B            | 2021-01-11  | 1           |
| B            | 2021-01-16  | 3           |
| B            | 2021-02-01  | 3           |
| C            | 2021-01-01  | 3           |
| C            | 2021-01-01  | 3           |
| C            | 2021-01-07  | 3           |

**Menu** Table

| product\_id | product\_name | price |
| ----------- | ------------- | ----- |
| 1           | sushi         | 10    |
| 2           | curry         | 15    |
| 3           | ramen         | 12    |

**Members** Table

| customer\_id | join\_date |
| ------------ | ---------- |
| A            | 2021-01-07 |
| B            | 2021-01-09 |

and I'm expecting to get&#x20;

**Expected Result**

| customer\_id | product\_name | order\_date |
| ------------ | ------------- | ----------- |
| A            | sushi         | 2021-01-01  |
| B            | curry         | 2021-01-01  |
| C            | ramen         | 2021-01-01  |

```sql
WITH ranked AS (
  SELECT 
    m.product_name, 
    s.customer_id, 
    s.order_date, 
    DENSE_RANK() OVER(
      PARTITION BY s.customer_id 
      ORDER BY 
        s.order_date, 
        s.product_id
    ) rank 
  FROM 
    dannys_diner.sales as s 
    JOIN dannys_diner.menu as m ON m.product_id = s.product_id
)
-- SELECT * FROM ranked # for testing the CTE(common table expression)
SELECT 
  customer_id, 
  product_name 
FROM 
  ranked 
WHERE 
  rank = 1 
GROUP BY 
  customer_id, 
  product_name
```

* Created a temp table `ranked` and use **Windows function** with **DENSE\_RANK** to create a new column `rank` which will have the ranking of each sales based on `order_date` and `product_id` .&#x20;
* Instead of **ROW\_NUMBER** or **RANK**, use **DENSE\_RANK** as `order_date` is not time-stamped hence, there is no sequence as to which item is ordered first if 2 or more items are ordered on the same day.
* Finally, just get the rank 1 which is `rank = 1` and **GROUP BY** all columns.
