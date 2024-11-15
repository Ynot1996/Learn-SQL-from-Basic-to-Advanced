---
# SQL JOIN 用法簡介

假設有兩個表 `customers` 和 `orders`，下方顯示了各種 JOIN 類型的用法、語法範例以及預期的輸出。

| JOIN TYPE       | Description                                   | Sample SQL Syntax                                                                                                               |
|-----------------|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| `INNER JOIN`    | 僅返回兩個表中符合條件的匹配記錄。                  | `SELECT customers.customer_name, orders.amount FROM customers INNER JOIN orders ON customers.customer_id = orders.customer_id;` |
| `LEFT JOIN`     | 返回左表中所有記錄,即使在右表中沒有匹配。            | `SELECT customers.customer_name, orders.amount FROM customers LEFT JOIN orders ON customers.customer_id = orders.customer_id;`  |
| `RIGHT JOIN`    | 返回右表中所有記錄,即使在左表中沒有匹配。            | `SELECT customers.customer_name, orders.amount FROM customers RIGHT JOIN orders ON customers.customer_id = orders.customer_id;` |
| `FULL JOIN`     | 返回兩表中所有記錄,包括不匹配的記錄。＝LEFT＋RIGHT   | `SELECT customers.customer_name, orders.amount FROM customers FULL JOIN orders ON customers.customer_id = orders.customer_id;`  |
| `CROSS JOIN`    | 返回兩個表的直積,即每一行與另一表的每一行組合。       | `SELECT customers.customer_name, orders.amount FROM customers CROSS JOIN orders;`                                               |
| `SELF JOIN`     | 表與自身進行連接,以比較或關聯同表中的不同記錄。       | `SELECT a.customer_name AS name1, b.customer_name AS name2 FROM customers a, customers b WHERE a.customer_id != b.customer_id;` |

## 原始表格

>

### `customers`
| customer_id | customer_name |
|-------------|---------------|
| 1           | Alice         |
| 2           | Bob           |
| 3           | Carol         |

### `orders`
| order_id | customer_id | amount |
|----------|-------------|--------|
| 101      | 1           | 200    |
| 102      | 2           | 150    |
| 103      | 4           | 300    |

## 預期輸出

### `INNER JOIN`
`SELECT customers.customer_name, orders.amount`<br> 
`FROM customers`<br> 
`INNER JOIN orders ON customers.customer_id = orders.customer_id;` 
| customer_name | amount |
|---------------|--------|
| Alice         | 200    |
| Bob           | 150    |

### `LEFT JOIN`
`SELECT customers.customer_name, orders.amount`<br> 
`FROM customers`<br>
`LEFT JOIN orders ON customers.customer_id = orders.customer_id;`
| customer_name | amount |
|---------------|--------|
| Alice         | 200    |
| Bob           | 150    |
| Carol         | NULL   |

### `RIGHT JOIN`
`SELECT customers.customer_name, orders.amount`<br> 
`FROM customers`<br>
`RIGHT JOIN orders ON customers.customer_id = orders.customer_id;`
| customer_name | amount |
|---------------|--------|
| Alice         | 200    |
| Bob           | 150    |
| NULL          | 300    |

### `FULL JOIN`
`SELECT customers.customer_name, orders.amount`<br> 
`FROM customers`<br> 
`FULL JOIN orders ON customers.customer_id = orders.customer_id;`
| customer_name | amount |
|---------------|--------|
| Alice         | 200    |
| Bob           | 150    |
| Carol         | NULL   |
| NULL          | 300    |

### `CROSS JOIN`
`SELECT customers.customer_name, orders.amount`<br> 
`FROM customers`<br>
`CROSS JOIN orders;`
| customer_name | amount |
|---------------|--------|
| Alice         | 200    |
| Alice         | 150    |
| Alice         | 300    |
| Bob           | 200    |
| Bob           | 150    |
| Bob           | 300    |
| Carol         | 200    |
| Carol         | 150    |
| Carol         | 300    |

### `SELF JOIN`
`SELECT a.customer_name AS name1, b.customer_name AS name2`<br> 
`FROM customers a, customers b`<br>
`WHERE a.customer_id != b.customer_id;`
| name1 | name2 |
|-------|-------|
| Alice | Bob   |
| Alice | Carol |
| Bob   | Alice |
| Bob   | Carol |
| Carol | Alice |
| Carol | Bob   |

---
