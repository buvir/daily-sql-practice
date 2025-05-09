# SQL 50 - LeetCode  
Solutions for SQL 50 Study Plan on LeetCode  

# ****Select****

#### **URL**
```markdown
https://leetcode.com/studyplan/top-sql-50/
````

#### **1757 - Recyclable and Low Fat Products**
```markdown
SELECT product_id  
FROM Products  
WHERE low_fats = 'Y'  
AND recyclable = 'Y'  
````

#### **584. Find Customer Referee**
```markdown
Select name from Customer  where referee_id != 2 OR referee_id is null
````

#### **595. Big Countries**
```markdown
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;
````


#### **1148. Article Views I**
```markdown
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id ASC;
````
#### **1683. Invalid Tweets**
```markdown
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
````
# ****Basic Joins****


#### **1378. Replace Employee ID With The Unique Identifier**
```markdown
Select u.unique_id ,e.name from Employees as e 
Left join EmployeeUNI as u
on e.id=u.id
````

#### **1068. Product Sales Analysis I**
```markdown
select p.product_name ,s.year  ,s.price from Sales as s
inner join Product as  p 
on s.product_id  =p.product_id 
````

#### **1581. Customer Who Visited but Did Not Make Any Transactions**
```markdown
Select v.customer_id ,count(v.visit_id  ) AS count_no_trans
from Visits as v
Left Join Transactions as t 
on v.visit_id =t.visit_id 
WHERE
t.transaction_id IS NULL
group by v.customer_id
ORDER BY 
    count_no_trans DESC;
````

#### **197. Rising Temperature**
```markdown
SELECT
    w1.id
FROM
    Weather w1
JOIN
    Weather w2 ON w1.recordDate = w2.recordDate + INTERVAL '1 day'
WHERE
    w1.temperature > w2.temperature;
````


#### **1661. Average Time of Process per Machine**
```markdown
WITH ProcessTimes AS (
    SELECT
        machine_id,
        process_id,
        MAX(CASE WHEN activity_type = 'end' THEN timestamp END) - MIN(CASE WHEN activity_type = 'start' THEN timestamp END) AS process_duration
    FROM
        Activity
    GROUP BY
        machine_id,
        process_id
)
SELECT
    machine_id,
    ROUND(AVG(process_duration)::numeric, 3) AS processing_time
FROM
    ProcessTimes
GROUP BY
    machine_id;
````

#### **577. Employee Bonus**
```markdown
Select e.name,b.bonus from Employee e
Left  join Bonus b
on e.empId =b.empId 
where bonus < 1000 or bonus is null
````

#### **1280. Students and Examinations**
```markdown
SELECT
    s.student_id,
    s.student_name,
    sub.subject_name,
    COUNT(e.subject_name) AS attended_exams
FROM
    Students s
CROSS JOIN
    Subjects sub
LEFT JOIN
    Examinations e ON s.student_id = e.student_id AND sub.subject_name = e.subject_name
GROUP BY
    s.student_id,
    s.student_name,
    sub.subject_name
ORDER BY
    s.student_id,
    sub.subject_name;
````


#### **570. Managers with at Least 5 Direct Reports**
```markdown
Select e1.name from Employee e1
JOIN
    Employee e2
     ON e1.id  = e2.managerId 
GROUP BY
    e1.id, e1.name
HAVING
    COUNT(e2.id) >= 5;
````

#### **1934. Confirmation Rate**
```markdown
WITH ConfirmationCounts AS (
    SELECT
        user_id,
        SUM(CASE WHEN action = 'confirmed' THEN 1 ELSE 0 END) AS confirmed_count,
        COUNT(*) AS total_count
    FROM
        Confirmations
    GROUP BY
        user_id
)
SELECT
    s.user_id,
    COALESCE(ROUND(CAST(cc.confirmed_count AS DECIMAL) / cc.total_count, 2), 0.00) AS confirmation_rate
FROM
    Signups s
LEFT JOIN
    ConfirmationCounts cc ON s.user_id = cc.user_id;
````

# ****Basic Aggregate Functions****

#### **620. Not Boring Movies**
```markdown
Select id,movie,description ,rating  from Cinema 
where id % 2 != 0 AND  description !='boring'
order by rating desc
````

#### **1251. Average Selling Price**
```markdown
WITH ProductSales AS (
    SELECT
        p.product_id,
        p.price,
        u.units,
        u.purchase_date
    FROM
        Prices p
    JOIN
        UnitsSold u ON p.product_id = u.product_id
    WHERE u.purchase_date BETWEEN p.start_date AND p.end_date
),
ProductRevenue AS (
    SELECT
        product_id,
        SUM(price * units) AS total_revenue,
        SUM(units) AS total_units_sold
    FROM
        ProductSales
    GROUP BY
        product_id
)
SELECT
    p.product_id,
    COALESCE(ROUND(CAST(pr.total_revenue AS DECIMAL) / pr.total_units_sold, 2), 0.00) AS average_price
FROM
    Prices p
LEFT JOIN
    ProductRevenue pr ON p.product_id = pr.product_id
GROUP BY p.product_id, pr.total_revenue, pr.total_units_sold
ORDER BY
    p.product_id;
````


#### **1075. Project Employees I**
```markdown
SELECT
    p.project_id,
    ROUND(AVG(e.experience_years), 2) AS average_years
FROM
    Project p
JOIN
    Employee e ON p.employee_id = e.employee_id
GROUP BY
    p.project_id;
````


#### **1633. Percentage of Users Attended a Contest**
```markdown
WITH ContestUserCounts AS (
    SELECT
        r.contest_id,
        COUNT(DISTINCT r.user_id) AS num_registered_users
    FROM
        Register r
    GROUP BY
        r.contest_id
),
TotalUserCount AS (
    SELECT
        COUNT(user_id) AS total_users
    FROM
        Users
)
SELECT
    c.contest_id,
    ROUND(
        (CAST(c.num_registered_users AS DECIMAL) / t.total_users) * 100,
        2
    ) AS percentage
FROM
    ContestUserCounts c,
    TotalUserCount t
ORDER BY
    percentage DESC,
    c.contest_id ASC;

````


#### **1075. Project Employees I**
```markdown
SELECT
    p.project_id,
    ROUND(AVG(e.experience_years), 2) AS average_years
FROM
    Project p
JOIN
    Employee e ON p.employee_id = e.employee_id
GROUP BY
    p.project_id;
````
#### **1211. Queries Quality and Percentage**
```
SELECT
    query_name,
    CAST(AVG(rating * 1.0 / position) AS DECIMAL(10,2)) AS quality,
    CAST(SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END) * 100.0 / COUNT(*) AS DECIMAL(10,2)) AS poor_query_percentage
FROM
    Queries
GROUP BY
    query_name;

```
