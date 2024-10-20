# Game Sales and Ratings Analysis - SQL Queries

## Overview

This repository contains a set of SQL queries designed to analyze video game sales and ratings, with a focus on identifying top-selling games, highly rated years in terms of critic scores, and comparing critic vs. user ratings for specific years. Each query provides insight into different aspects of game sales and their corresponding reviews.

### Queries

1. **Best Selling Games** (`best_selling_games`):
   This query retrieves the top 10 best-selling video games based on the total number of copies sold.
   
   **Query:**
   ```sql
   SELECT * FROM game_sales 
   ORDER BY games_sold DESC
   LIMIT 10;
   ```

   - **Table:** `game_sales`
   - **Columns:** All columns from the `game_sales` table.
   - **Sorting:** The results are sorted by `games_sold` in descending order.
   - **Limit:** Displays the top 10 games based on sales.

2. **Critics' Top Ten Years** (`critics_top_ten_years`):
   This query finds the top 10 years with the highest average critic scores for games, where at least 5 games were released. The results are grouped by year and sorted by the average critic score.
   
   **Query:**
   ```sql
   SELECT g.year, 
          COUNT(g.name) AS num_games, 
          ROUND(AVG(r.critic_score), 2) AS avg_critic_score
   FROM game_sales g
   INNER JOIN reviews r USING (name)
   GROUP BY g.year
   HAVING COUNT(g.name) > 4
   ORDER BY avg_critic_score DESC
   LIMIT 10;
   ```

   - **Tables:** `game_sales` and `reviews`
   - **Columns Returned:**
     - `year`: Year of the games.
     - `num_games`: Number of games released in that year.
     - `avg_critic_score`: The average critic score for that year's games (rounded to 2 decimal places).
   - **Conditions:** Only years with more than 4 games are considered.
   - **Sorting:** The results are sorted by average critic score in descending order.
   - **Limit:** Displays the top 10 years based on critic scores.

3. **Golden Years of Gaming** (`golden_years`):
   This query compares the average critic score and average user score for specific years and calculates the difference between them. The results show years where either the critic score or the user score is greater than 9.
   
   **Query:**
   ```sql
   SELECT c.year, 
          c.num_games, 
          c.avg_critic_score, 
          u.avg_user_score, 
          (c.avg_critic_score - u.avg_user_score) AS diff
   FROM critics_avg_year_rating c 
   INNER JOIN users_avg_year_rating u USING (year)
   WHERE c.avg_critic_score > 9 
      OR u.avg_user_score > 9
   ORDER BY c.year;
   ```

   - **Tables:** `critics_avg_year_rating` and `users_avg_year_rating`
   - **Columns Returned:**
     - `year`: The year of the games.
     - `num_games`: The number of games released in that year.
     - `avg_critic_score`: The average critic score for that year.
     - `avg_user_score`: The average user score for that year.
     - `diff`: The difference between the average critic score and the average user score.
   - **Conditions:** Displays years where either the critic score or the user score is greater than 9.
   - **Sorting:** The results are sorted by year in ascending order.
## Usage
1. Run the queries in your SQL environment against the appropriate tables to generate insights about top-selling games, highly rated years, and critic-user score differences.
2. Adjust the queries as needed for your specific data and analysis requirements.