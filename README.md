# Eurovision SQL Analysis

## Overview

Analysis of 60+ years of Eurovision Song Contest (1957–2022) using SQL in Google BigQuery. The dataset contains 1,359 records across 51 countries. The project covers performance trends, decade-by-decade comparisons, and year-over-year analysis using window functions.

## Dataset

The dataset contains information about:

* Country
* Performer
* Song
* Year
* Points
* Placement

## Analysis Performed

1. Countries with the highest average points
2. Performers with multiple wins
3. Country rankings by total points
4. Participation trends
5. Average points by decade
6. Top scoring songs
7. High-performing performers
8. Decade rankings
9. Countries by participation count
10. Countries above overall average
11. Before vs After 2000 comparison
12. Performer rankings by year
13. How did each country's points change compared to their previous appearance?
14. For each performance, compare with the next appearance of the same country
    
## Skills Demonstrated

* Aggregations
* GROUP BY
* HAVING
* Window Functions
* CTEs
* Subqueries
* Ranking Functions
* LAG/LEAD

## Key Findings

* Points inflation is real: average score grew from ~10 (1950s) to ~180 (2020s)
* Ukraine finished in Top 5 eight times despite competing since 2003
* Salvador Sobral (Portugal, 2017) holds the all-time record with 758 points
* Western European "Big 5" dominate participation count but not average points
  
## Files

* queries.sql
