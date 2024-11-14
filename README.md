# SQL JOIN 用法簡介

假設有兩個表 `customers` 和 `orders`，下方顯示了各種 JOIN 類型的用法、語法範例以及預期的輸出。

| JOIN 類型       | 說明                                                                                  | 範例 SQL 語法                                                                                                       |
|-----------------|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `INNER JOIN`    | 僅返回兩個表中符合條件的匹配記錄。                                                    | `SELECT customers.customer_name, orders.amount FROM customers INNER JOIN orders ON customers.customer_id = orders.customer_id;` |
| `LEFT JOIN`     | 返回左表中的所有記錄，即使在右表中沒有匹配。                                          | `SELECT customers.customer_name, orders.amount FROM customers LEFT JOIN orders ON customers.customer_id = orders.customer_id;`  |
| `RIGHT JOIN`    | 返回右表中的所有記錄，即使在左表中沒有匹配。                                          | `SELECT customers.customer_name, orders.amount FROM customers RIGHT JOIN orders ON customers.customer_id = orders.customer_id;` |
| `FULL JOIN`     | 返回兩個表中的所有記錄，包括不匹配的記錄（LEFT JOIN + RIGHT JOIN）。                  | `SELECT customers.customer_name, orders.amount FROM customers FULL JOIN orders ON customers.customer_id = orders.customer_id;`  |
| `CROSS JOIN`    | 返回兩個表的笛卡爾積，即每一行與另一表的每一行組合。                                 | `SELECT customers.customer_name, orders.amount FROM customers CROSS JOIN orders;`                                     |
| `SELF JOIN`     | 一個表與自身連接，用於比較同一表的不同記錄。                                          | `SELECT a.customer_name AS name1, b.customer_name AS name2 FROM customers a, customers b WHERE a.customer_id != b.customer_id;` |

---

### customers 表的資料
| customer_id | customer_name |
|-------------|---------------|
| 1           | Alice         |
| 2           | Bob           |
| 3           | Carol         |

### orders 表的資料
| order_id | customer_id | amount |
|----------|-------------|--------|
| 101      | 1           | 200    |
| 102      | 2           | 150    |
| 103      | 4           | 300    |

---



### 預期輸出

#### `INNER JOIN`
| customer_name | amount |
|---------------|--------|
| Alice         | 200    |
| Bob           | 150    |

#### `LEFT JOIN`
| customer_name | amount |
|---------------|--------|
| Alice         | 200    |
| Bob           | 150    |
| Carol         | NULL   |

#### `RIGHT JOIN`
| customer_name | amount |
|---------------|--------|
| Alice         | 200    |
| Bob           | 150    |
| NULL          | 300    |

#### `FULL JOIN`
| customer_name | amount |
|---------------|--------|
| Alice         | 200    |
| Bob           | 150    |
| Carol         | NULL   |
| NULL          | 300    |

#### `CROSS JOIN`
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

#### `SELF JOIN`
| name1 | name2 |
|-------|-------|
| Alice | Bob   |
| Alice | Carol |
| Bob   | Alice |
| Bob   | Carol |
| Carol | Alice |
| Carol | Bob   |
