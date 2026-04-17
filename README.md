# 🎬 Netflix Data Analysis

## 📌 Overview
Analyzed Netflix dataset using SQL and built an interactive Power BI dashboard to uncover trends and insights.

## 🛠 Tools Used
- MySQL  
- Power BI  

## 📊 Key Insights
- Movies dominate over TV Shows  
- United States produces the most content  
- Content increased rapidly after 2015  
- TV-MA is the most common rating  

## 📷 Dashboard
![Dashboard](dashboard.png)

## 🧠 SQL Analysis
```sql
SELECT type, COUNT(*) FROM netflix GROUP BY type;

SELECT country, COUNT(*) 
FROM netflix
GROUP BY country
ORDER BY COUNT(*) DESC
LIMIT 10;

SELECT release_year, COUNT(*) 
FROM netflix
GROUP BY release_year;

SELECT rating, COUNT(*) 
FROM netflix
GROUP BY rating;
```

> Full queries available in `queries.sql`

## 🚀 Conclusion
This project demonstrates data cleaning, analysis, and visualization using SQL and Power BI.
