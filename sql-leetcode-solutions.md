# SQL 50 - LeetCode  
Solutions for SQL 50 Study Plan on LeetCode  


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
