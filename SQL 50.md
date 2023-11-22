**SELECT PROBLEMS**

**[1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/?envType=study-plan-v2&envId=top-sql-50)**

Table: Products

| Column Name | Type    |
|-------------|---------|
| product_id  | int     |
| low_fats    | enum    |
| recyclable  | enum    |

product_id is the primary key (column with unique values) for this table.
low_fats is an ENUM (category) of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
recyclable is an ENUM (category) of types ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.
 

Write a solution to find the ids of products that are both low fat and recyclable.

Return the result table in any order.

**Solution:**
```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
AND recyclable = 'Y'; 
```

**[584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/?envType=study-plan-v2&envId=top-sql-50)**

Table: Customer

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| referee_id  | int     |

In SQL, id is the primary key column for this table.
Each row of this table indicates the id of a customer, their name, and the id of the customer who referred them.
 
Find the names of the customer that are not referred by the customer with id = 2.

Return the result table in any order.

**Solution:**
```sql
SELECT name
FROM Customer
WHERE referee_id <> 2 
OR referee_id IS NULL;
```

**[595. Big Countries](https://leetcode.com/problems/big-countries/)**

Table: World

| Column Name | Type    |
|-------------|---------|
| name        | varchar |
| continent   | varchar |
| area        | int     | 
| population  | int     |
| gdp         | bigint  |

name is the primary key (column with unique values) for this table.
Each row of this table gives information about the name of a country, the continent to which it belongs, its area, the population, and its GDP value.

**Solution:**
```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000
OR population >= 25000000;
```

**[595. Article Views I](https://leetcode.com/problems/article-views/)**

Table: Views

| Column Name | Type    |
|-------------|---------|
| article_id  | int     |
| author_id   | int     |
| viewer_id   | int     | 
| view_date   | date    |

There is no primary key (column with unique values) for this table, the table may have duplicate rows.
Each row of this table indicates that some viewer viewed an article (written by some author) on some date. 
Note that equal author_id and viewer_id indicate the same person.

Write a solution to find all the authors that viewed at least one of their own articles.

Return the result table sorted by id in ascending order.

**Solution:**
```sql
SELECT DISTINCT author_id AS id FROM Views
WHERE article_id >= 1
AND author_id = viewer_id
ORDER BY author_id ASC;
```

**[1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/?envType=study-plan-v2&envId=top-sql-50)**

Table: Tweets

| Column Name | Type    |
|-------------|---------|
| tweet_id    | int     |
| content     | varchar |

tweet_id is the primary key (column with unique values) for this table.
This table contains all the tweets in a social media app.

Write a solution to find the IDs of the invalid tweets. The tweet is invalid if the number of characters used in the content of the tweet is strictly greater than 15.

Return the result table in any order.

**Solution:**
```sql
SELECT tweet_id FROM Tweets 
WHERE LENGTH(content) > 15;
```

**BASIC JOINS**

**[1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/?envType=study-plan-v2&envId=top-sql-50)**

Table: Employees

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |

id is the primary key (column with unique values) for this table.
Each row of this table contains the id and the name of an employee in a company.

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| unique_id   | int     |

(id, unique_id) is the primary key (combination of columns with unique values) for this table.
Each row of this table contains the id and the corresponding unique id of an employee in the company.

Write a solution to show the unique ID of each user, If a user does not have a unique ID replace just show null.

Return the result table in any order.

**Solution:**
```sql
SELECT unique_id, name
FROM Employees
LEFT JOIN EmployeeUNI
ON Employees.id = EmployeeUNI.id;
```

**[1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/?envType=study-plan-v2&envId=top-sql-500)**

Table: Sales

| Column Name | Type    |
|-------------|---------|
| sale_id     | int     |
| product_id  | int     |
| year        | int     |
| quantity    | int     |
| price       | int     |

(sale_id, year) is the primary key (combination of columns with unique values) of this table.
product_id is a foreign key (reference column) to Product table.
Each row of this table shows a sale on the product product_id in a certain year.
Note that the price is per unit.

Table: Product

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

product_id is the primary key (column with unique values) of this table.
Each row of this table indicates the product name of each product.

Write a solution to report the product_name, year, and price for each sale_id in the Sales table.

Return the resulting table in any order.

**Solution:**
```sql
SELECT product_name, year, price 
FROM Sales 
LEFT JOIN Product 
ON Sales.product_id = Product.product_id;
```




