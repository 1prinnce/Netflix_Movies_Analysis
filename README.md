# Netflix Data Analysis Project

## 📌 Overview
This project analyzes the Netflix dataset using SQL and visualizes insights using Power BI.

---

## 🛠 Tools Used
- MySQL
- Power BI

---

## 📊 Key Insights
- Movies dominate over TV Shows  
- Most content is produced by the United States  
- Content increased rapidly after 2015  
- TV-MA is the most common rating  

---

## 📷 Dashboard
![Dashboard](dashboard.png)

---

## 🧠 SQL Queries Used

```sql
-- ==============================
-- 1. BASIC UNDERSTANDING
-- ==============================

SELECT * FROM netflix LIMIT 10;

SELECT COUNT(*) FROM netflix;

SELECT DISTINCT type FROM netflix;


-- ==============================
-- 2. DATA CLEANING
-- ==============================

SELECT * FROM netflix WHERE director IS NULL;

UPDATE netflix
SET director = 'Unknown'
WHERE director IS NULL;


-- ==============================
-- 3. BASIC ANALYSIS
-- ==============================

-- Movies vs TV Shows
SELECT type, COUNT(*) 
FROM netflix 
GROUP BY type;

-- Top 10 countries
SELECT country, COUNT(*) AS total
FROM netflix
GROUP BY country
ORDER BY total DESC
LIMIT 10;

-- Most common genres
SELECT listed_in, COUNT(*) 
FROM netflix
GROUP BY listed_in
ORDER BY COUNT(*) DESC;

-- Year-wise content
SELECT release_year, COUNT(*) 
FROM netflix
GROUP BY release_year
ORDER BY release_year;

-- Latest content
SELECT title, date_added
FROM netflix
ORDER BY date_added DESC;

-- Movies only
SELECT title, duration
FROM netflix
WHERE type = 'Movie';


-- ==============================
-- 4. INTERMEDIATE ANALYSIS
-- ==============================

-- New vs Old content
SELECT 
    COUNT(*) AS total,
    CASE 
        WHEN release_year >= 2020 THEN 'New'
        ELSE 'Old'
    END AS category
FROM netflix
GROUP BY category;

-- Top recent years
SELECT release_year, COUNT(*) AS total
FROM netflix
GROUP BY release_year
ORDER BY release_year DESC
LIMIT 5;

-- Director analysis
SELECT director, COUNT(*) 
FROM netflix
GROUP BY director
ORDER BY COUNT(*) DESC
LIMIT 10;


-- ==============================
-- 5. ADVANCED ANALYSIS
-- ==============================

-- Year-wise Movies vs TV Shows
SELECT release_year, type, COUNT(*) AS total
FROM netflix
GROUP BY release_year, type
ORDER BY release_year;

-- Recent country trend (after 2018)
SELECT country, COUNT(*) AS total
FROM netflix
WHERE release_year >= 2018
GROUP BY country
ORDER BY total DESC
LIMIT 10;

-- Longest movies
SELECT title, duration
FROM netflix
WHERE type = 'Movie'
ORDER BY CAST(SUBSTRING_INDEX(duration, ' ', 1) AS UNSIGNED) DESC
LIMIT 10;

-- Most active directors (excluding Unknown)
SELECT director, COUNT(*) AS total
FROM netflix
WHERE director != 'Unknown'
GROUP BY director
ORDER BY total DESC
LIMIT 10;

-- Content added per year
SELECT YEAR(STR_TO_DATE(date_added, '%M %d, %Y')) AS year, COUNT(*) AS total
FROM netflix
GROUP BY year
ORDER BY year;

-- Rating distribution
SELECT rating, COUNT(*) AS total
FROM netflix
GROUP BY rating
ORDER BY total DESC;

-- Movies longer than 2 hours
SELECT title, duration
FROM netflix
WHERE type = 'Movie'
AND CAST(SUBSTRING_INDEX(duration, ' ', 1) AS UNSIGNED) > 120;
