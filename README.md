# Hacker News Data Analysis Project

## Project Overview

This project showcases SQL queries used to analyze a dataset from Hacker News, a popular tech news aggregator site. The dataset contains information such as story titles, scores, users, URLs, and timestamps. The project explores various techniques to extract insights, including retrieving top stories, calculating sums, aggregating scores by users, and analyzing data by source and time.

## Required Skills

To work with and understand this project, the following skills are essential:

### 1. **SQL Basics**
   - **Querying data**: Using `SELECT`, `WHERE`, `LIMIT` to retrieve data.
   - **Aggregations**: Understanding `SUM()`, `COUNT()`, `AVG()`, and `MAX()` to perform calculations on the data.
   - **Ordering and Grouping**: Using `ORDER BY` to sort results, and `GROUP BY` to categorize data for analysis.

### 2. **Advanced SQL**
   - **Conditional Logic**: The use of `CASE` statements for dynamic column generation based on conditions.
   - **Filtering Groups**: Using `HAVING` to filter aggregated results (e.g., users with a total score above 200).
   - **String Pattern Matching**: Using `LIKE` to filter URLs based on patterns (e.g., finding specific video URLs).

### 3. **Date and Time Functions**
   - **Extracting Parts of Timestamps**: Using `strftime()` to extract specific components (like the hour) from timestamp data for time-based analysis.

### 4. **Mathematical Operations**
   - **Arithmetic Calculations**: Ability to perform basic mathematical calculations on the data (e.g., `(517 + 309 + 304 + 282) / 6366.0`).


## SQL Queries and Their Purpose

### 1. **Top 5 Stories by Score**
```sql
SELECT title, score
FROM hacker_news
ORDER BY score DESC
LIMIT 5;
```
- **Purpose**: Retrieves the top 5 stories based on their score. This gives insight into the highest-rated posts on Hacker News.

### 2. **Total Score of All Stories**
```sql
SELECT SUM(score) FROM hacker_news;
```
- **Purpose**: Calculates the total score across all stories, providing an overall measure of engagement on the platform.

### 3. **Users with a Total Score Above 200**
```sql
SELECT user, SUM(score) FROM hacker_news
GROUP BY user
HAVING SUM(score) > 200
ORDER BY 2 DESC;
```
- **Purpose**: Lists users who have contributed stories with a combined score of over 200, ordered by their total score.

### 4. **Custom Calculation**
```sql
SELECT (517 + 309 + 304 + 282) / 6366.0;
```
- **Purpose**: This is a custom arithmetic operation calculating the average of selected scores divided by the total number of stories. This type of operation is often used for quick, ad-hoc calculations.

### 5. **Count Stories with a Specific URL (e.g., Rickroll)**
```sql
SELECT user, COUNT(*) 
FROM hacker_news
WHERE url LIKE '%watch?v=dQw4w9WgXcQ%' 
GROUP BY user;
```
- **Purpose**: Finds how many users posted a specific YouTube video (in this case, the infamous Rickroll). This shows how often certain URLs appear and who is posting them.

### 6. **Categorizing Sources Based on URLs**
```sql
SELECT CASE
   WHEN url LIKE '%github.com%' THEN 'GitHub'
   WHEN url LIKE '%medium.com%' THEN 'Medium'
   WHEN url LIKE '%nytimes.com%' THEN 'New York Times'
   ELSE 'Other'
  END AS 'Source', COUNT(*)
FROM hacker_news
GROUP BY 1;
```
- **Purpose**: Categorizes stories by their source (e.g., GitHub, Medium, New York Times) based on the URL structure. The `CASE` statement allows dynamic categorization and the count of stories from each source.

### 7. **Retrieve Timestamps**
```sql
SELECT timestamp
FROM hacker_news
LIMIT 10;
```
- **Purpose**: Retrieves the first 10 timestamps from the dataset, which can be useful for preliminary data inspection.

### 8. **Extract Hour from Timestamps**
```sql
SELECT timestamp, 
   strftime('%H', timestamp)
FROM hacker_news
GROUP BY 1
LIMIT 20;
```
- **Purpose**: Extracts the hour from the timestamps of stories, which helps analyze posting trends by time of day.

### 9. **Average Score by Hour of the Day**
```sql
SELECT strftime('%H', timestamp) AS 'Hour', 
        ROUND(AVG(score), 1) AS 'Average Score',
        COUNT(*) AS 'Number of Stories'
FROM hacker_news
WHERE timestamp IS NOT NULL
GROUP BY 1;
```
- **Purpose**: Groups stories by the hour they were posted, calculates the average score for each hour, and counts how many stories were posted during each hour. This helps identify high-engagement times.


## How to Use This Project

1. **Dataset**: 
   - Ensure you have access to a dataset named `hacker_news`, which contains columns like `title`, `score`, `user`, `url`, and `timestamp`.

2. **Running the Queries**: 
   - Use an SQL database management tool (such as SQLite, MySQL, or PostgreSQL) to run the provided queries and explore the results.

3. **Modify and Extend**: 
   - Feel free to modify the queries to suit your dataset or add more analytical queries to gain deeper insights.

## Conclusion

This project demonstrates various SQL techniques for analyzing data from a popular tech news platform, Hacker News. By combining aggregation, conditional logic, and time-based analysis, you can gain meaningful insights from the dataset and showcase my ability to work with real-world data in SQL.
