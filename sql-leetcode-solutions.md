# SQL 50 - LeetCode  
Solutions for SQL 50 Study Plan on LeetCode  

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


