**I. SELECT PROBLEMS**

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

**II. BASIC JOINS**

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

**[1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/?envType=study-plan-v2&envId=top-sql-50)**

Table: Visits

| Column Name  | Type    |
|--------------|---------|
| visit_id     | int     |
| customer_id  | int     |

visit_id is the column with unique values for this table.
This table contains information about the customers who visited the mall.

Table: Transactions

| Column Name     | Type    |
|-----------------|---------|
| transaction_id  | int     |
| visit_id        | int     |
| amount          | int     |

transaction_id is column with unique values for this table.
This table contains information about the transactions made during the visit_id.

Write a solution to find the IDs of the users who visited without making any transactions and the number of times they made these types of visits.

Return the result table sorted in any order.

**Solution:**
```sql
SELECT customer_id, COUNT(customer_id) AS count_no_trans
FROM Visits
LEFT JOIN Transactions ON visits.visit_id = transactions.visit_id
WHERE amount IS NULL
GROUP by customer_id;
```

**[197. Rising Temperature](https://leetcode.com/problems/rising-temperature/?envType=study-plan-v2&envId=top-sql-50)**

Table: Weather

| Column Name  | Type    |
|--------------|---------|
| id           | int     |
| recordDate   | date    |
| temperature  | int     |

id is the column with unique values for this table.
This table contains information about the temperature on a certain day.

Write a solution to find all dates' Id with higher temperatures compared to its previous dates (yesterday).

Return the result table in any order.

**Solution:**
```sql
SELECT a.Id
FROM Weather a, Weather b
WHERE DATEDIFF(a.recordDate , b.recordDate) = 1
AND a.temperature > b.temperature;
```

**[577. Employee Bonus](https://leetcode.com/problems/employee-bonus/?envType=study-plan-v2&envId=top-sql-50)**

Table: Employee

| Column Name  | Type    |
|--------------|---------|
| empId        | int     |
| name         | varchar |
| supervisor   | int     |
| salary       | int     |

empId is the column with unique values for this table.
Each row of this table indicates the name and the ID of an employee in addition to their salary and the id of their manager.

Table: Bonus

| Column Name  | Type    |
|--------------|---------|
| empId        | int     |
| bonus        | int     |

empId is the column of unique values for this table.
empId is a foreign key (reference column) to empId from the Employee table.
Each row of this table contains the id of an employee and their respective bonus.

Write a solution to report the name and bonus amount of each employee with a bonus less than 1000.

Return the result table in any order.

**Solution:**
```sql
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN BONUS b ON e.empId = b.empID
WHERE b.bonus < 1000 
OR b.bonus IS NULL;
```

**[1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/?envType=study-plan-v2&envId=top-sql-50)**

Table: Students

| Column Name   | Type    |
|---------------|---------|
| student_ID    | int     |
| student_name  | varchar |

student_id is the primary key (column with unique values) for this table.
Each row of this table contains the ID and the name of one student in the school.

Table: Subjects

| Column Name  | Type    |
|--------------|---------|
| subject_name | varchar |

subject_name is the primary key (column with unique values) for this table.
Each row of this table contains the name of one subject in the school.

Table: Examinations

| Column Name  | Type    |
|--------------|---------|
| student_id   | int     |
| subject_name | varchar |

There is no primary key (column with unique values) for this table. It may contain duplicates.
Each student from the Students table takes every course from the Subjects table.
Each row of this table indicates that a student with ID student_id attended the exam of subject_name

Write a solution to find the number of times each student attended each exam.

Return the result table ordered by student_id and subject_name.

**Solution:**
```sql
SELECT st.student_id , st.student_name,
su.subject_name,
COUNT(ex.student_id) AS attended_exams
FROM STUDENTS st
CROSS JOIN SUBJECTS su 
LEFT JOIN EXAMINATIONS ex ON st.student_id = ex.student_id
AND ex.subject_name = su.subject_name
GROUP BY st.student_id, su.subject_name
ORDER BY st.student_id;
```

**III. Basic Aggregate Functions**

**[620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/?envType=study-plan-v2&envId=top-sql-50)**

 Table: Cinema

| Column Name  | Type    |
|--------------|---------|
| id           | int     |
| movie        | varchar |
| description  | varchar |
| rating       | float   |

id is the primary key (column with unique values) for this table.
Each row contains information about the name of a movie, its genre, and its rating.
rating is a 2 decimal places float in the range [0, 10]

Write a solution to report the movies with an odd-numbered ID and a description that is not "boring".

Return the result table ordered by rating in descending order.

**Solution:**
```sql
SELECT * 
FROM Cinema
WHERE mod(id,2) <> 0
AND description != 'boring'
ORDER by rating DESC;
```

**[1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/?envType=study-plan-v2&envId=top-sql-50)**

 Table: Prices

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| start_date   | date    |
| end_date     | date    |
| price        | int     |

(product_id, start_date, end_date) is the primary key (combination of columns with unique values) for this table.
Each row of this table indicates the price of the product_id in the period from start_date to end_date.
For each product_id there will be no two overlapping periods. That means there will be no two intersecting periods for the same product_id.

 Table: UnitsSold

| Column Name   | Type    |
|---------------|---------|
| product_id    | int     |
| purchase_date | date    |
| units         | int     |

This table may contain duplicate rows.
Each row of this table indicates the date, units, and product_id of each product sold. 

Write a solution to find the average selling price for each product. average_price should be rounded to 2 decimal places.

Return the result table in any order.

**Solution:**
```sql
SELECT p.product_id,
ROUND(SUM(u.units * p.price) / SUM(u.units), 2) AS average_price
FROM PRICES p
LEFT JOIN UnitsSold u ON p.product_id = u.product_id
WHERE u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id; 
```

**IV. Sorting and Grouping**

**[1729. Find Followers Count](https://leetcode.com/problems/find-followers-count/?envType=study-plan-v2&envId=top-sql-50)**

 Table: Followers

| Column Name  | Type    |
|--------------|---------|
| user_id      | int     |
| follower_id  | int     |

(user_id, follower_id) is the primary key (combination of columns with unique values) for this table.
This table contains the IDs of a user and a follower in a social media app where the follower follows the user.

Write a solution that will, for each user, return the number of followers.

Return the result table ordered by user_id in ascending order.

**Solution:**
```sql
SELECT user_id, COUNT(follower_id) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id ASC;
```

**IV. Advanced Selects and Joins**

**[1731. The Number of Employees Which Report to Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/?envType=study-plan-v2&envId=top-sql-50)**

 Table: Employees

| Column Name  | Type    |
|--------------|---------|
| employee_id  | int     |
| name         | varchar |
| reports_to   | int     |
| age          | int     |

employee_id is the column with unique values for this table.
This table contains information about the employees and the id of the manager they report to. Some employees do not report to anyone (reports_to is null). 

For this problem, we will consider a manager an employee who has at least 1 other employee reporting to them.

Write a solution to report the ids and the names of all managers, the number of employees who report directly to them, and the average age of the reports rounded to the nearest integer.

Return the result table ordered by employee_id.

**Solution:**
```sql
SELECT
    em1.employee_id,
    em1.name,
    COUNT(em2.employee_id) AS reports_count,
    ROUND(AVG(em2.age)) AS average_age
FROM Employees AS em1
INNER JOIN Employees AS em2 ON em1.employee_id = em2.reports_to
GROUP BY em1.employee_id
ORDER BY em1.employee_id;
```







