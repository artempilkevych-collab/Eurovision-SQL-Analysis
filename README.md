# Eurovision-SQL-Analysis
--- 1. Which countries have the highest average points in Eurovision history?
SELECT country, AVG(points) AS avg_points
FROM testprod-440615.euro.test
GROUP BY 1
ORDER BY 2 DESC
--- 2. Which performer/group won more than one time 
SELECT performer,COUNT(*) AS wins
FROM testprod-440615.euro.test 
WHERE place LIKE '1 %'
GROUP BY 1
ORDER BY 2 DESC
--- 3. Rank countries by total Eurovision points earned across all years
SELECT country, SUM(points) AS total_points, RANK() OVER (ORDER BY SUM(points) DESC) AS rank_countries
FROM testprod-440615.euro.test 
GROUP BY 1
ORDER BY 2 DESC
---4. Which countries appeared in Eurovision the most times?
Select country, COUNT(*) AS participation_count
FROM testprod-440615.euro.test
GROUP BY 1
ORDER BY 2 DESC
---5. Which years had the highest average Eurovision points?
SELECT year, AVG(points) AS avf_points
FROM testprod-440615.euro.test
GROUP BY 1
Order by 2 DESC
---6. The top 5 highest-scoring songs of all time.
SELECT performer, song, SUM(points) AS total_points
FROM testprod-440615.euro.test
GROUP BY 1,2
ORDER BY 3 DESC
LIMIT 5
---7. Which performers received more than 350 points?
SELECT performer, SUM(points) AS total_points
FROM testprod-440615.euro.test
GROUP BY 1
HAVING SUM(points)>350
ORDER BY 2 DESC
---8. Which countries scored the highest total points in each decade?
WITH decade_points AS (
    SELECT
        country,
        CASE
            WHEN year BETWEEN 1950 AND 1959 THEN '1950s'
            WHEN year BETWEEN 1960 AND 1969 THEN '1960s'
            WHEN year BETWEEN 1970 AND 1979 THEN '1970s'
            WHEN year BETWEEN 1980 AND 1989 THEN '1980s'
            WHEN year BETWEEN 1990 AND 1999 THEN '1990s'
            WHEN year BETWEEN 2000 AND 2009 THEN '2000s'
            WHEN year BETWEEN 2010 AND 2019 THEN '2010s'
            WHEN year BETWEEN 2020 AND 2029 THEN '2020s'
        END AS decade,
        SUM(points) AS total_points
    FROM testprod-440615.euro.test
    GROUP BY country, decade
)
SELECT
    country,
    decade,
    total_points,
    RANK() OVER(PARTITION BY decade ORDER BY total_points DESC) AS ranking
FROM decade_points
ORDER BY decade, ranking;
----9. Which years had the largest number of participating countries?
SELECT year, COUNT(country) AS country_count
FROM testprod-440615.euro.test
GROUP BY 1
ORDER BY 2 DESC
---10. Countries whose average points are above the overall average.
SELECT country, AVG(points) AS avg_points
FROM testprod-440615.euro.test
GROUP BY 1
HAVING AVG(points) >(
  SELECT AVG(points) AS avg_points_overall
  FROM testprod-440615.euro.test
)
---11. Compare average Eurovision points before and after 2000
SELECT
    CASE
        WHEN year < 2000 THEN 'Before 2000'
        ELSE 'After 2000'
    END AS period,
    ROUND(AVG(points),2) AS avg_points
FROM testprod-440615.euro.test
GROUP BY period
ORDER BY avg_points DESC;
----12. Rank performers within each year
SELECT
    year,
    performer,
    country,
    points,
    RANK() OVER(PARTITION BY year ORDER BY points DESC) AS ranking
FROM testprod-440615.euro.test
ORDER BY year, ranking;
