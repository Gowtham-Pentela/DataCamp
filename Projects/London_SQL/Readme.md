# Transport Journeys Analysis - SQL Queries

## Overview

This repository contains SQL queries designed to analyze transportation journey data from the Transport for London (TFL) database. The queries provide insights into the most popular modes of transport, the usage of the Emirates Airline, and the least popular years for the London Underground. These analyses can help in understanding trends in public transport usage over time.

### Queries

1. **Most Popular Transport Types** (`most_popular_transport_types`):
   This query identifies the most popular types of journeys based on the total number of journeys (in millions) for each transport type.

   **Query:**
   ```sql
   SELECT JOURNEY_TYPE, 
          SUM(JOURNEYS_MILLIONS) AS TOTAL_JOURNEYS_MILLIONS
   FROM TFL.JOURNEYS
   GROUP BY JOURNEY_TYPE
   ORDER BY TOTAL_JOURNEYS_MILLIONS DESC;
   ```

   - **Table:** `TFL.JOURNEYS`
   - **Columns Returned:**
     - `JOURNEY_TYPE`: The type of transport (e.g., Bus, Underground, etc.).
     - `TOTAL_JOURNEYS_MILLIONS`: The total number of journeys in millions for each transport type.
   - **Grouping:** The data is grouped by `JOURNEY_TYPE` to sum the journeys for each transport type.
   - **Sorting:** The results are sorted in descending order by the total number of journeys to display the most popular transport types at the top.

2. **Emirates Airline Popularity** (`emirates_airline_popularity`):
   This query retrieves the months and years when the Emirates Airline saw its highest usage, displaying the top 5 months by the number of journeys (in millions).

   **Query:**
   ```sql
   SELECT MONTH, 
          YEAR, 
          ROUND(JOURNEYS_MILLIONS, 2) AS ROUNDED_JOURNEYS_MILLIONS
   FROM TFL.JOURNEYS
   WHERE JOURNEY_TYPE = 'Emirates Airline' 
     AND ROUNDED_JOURNEYS_MILLIONS IS NOT NULL
   ORDER BY ROUNDED_JOURNEYS_MILLIONS DESC
   LIMIT 5;
   ```

   - **Table:** `TFL.JOURNEYS`
   - **Columns Returned:**
     - `MONTH`: The month of the recorded journeys.
     - `YEAR`: The year of the recorded journeys.
     - `ROUNDED_JOURNEYS_MILLIONS`: The number of journeys (in millions), rounded to 2 decimal places.
   - **Conditions:** The query filters for journeys with the `JOURNEY_TYPE = 'Emirates Airline'` and excludes any null values for journey counts.
   - **Sorting:** The results are sorted by the number of journeys in descending order, showing the months with the highest usage of the Emirates Airline.
   - **Limit:** Displays the top 5 records.

3. **Least Popular Years for the London Underground** (`least_popular_years_tube`):
   This query finds the least popular years for the London Underground by calculating the total number of journeys (in millions) for each year and transport type, and then displaying the bottom 5 years in terms of total journeys.

   **Query:**
   ```sql
   SELECT YEAR, 
          JOURNEY_TYPE, 
          SUM(JOURNEYS_MILLIONS) AS TOTAL_JOURNEYS_MILLIONS
   FROM TFL.JOURNEYS
   WHERE JOURNEY_TYPE LIKE '%Underground%'
   GROUP BY YEAR, JOURNEY_TYPE
   ORDER BY TOTAL_JOURNEYS_MILLIONS ASC
   LIMIT 5;
   ```

   - **Table:** `TFL.JOURNEYS`
   - **Columns Returned:**
     - `YEAR`: The year of the recorded journeys.
     - `JOURNEY_TYPE`: The specific type of underground transport (e.g., London Underground, Underground Night Tube).
     - `TOTAL_JOURNEYS_MILLIONS`: The total number of journeys (in millions) for each year.
   - **Conditions:** Filters only transport types that include 'Underground' in the journey type.
   - **Grouping:** The data is grouped by both `YEAR` and `JOURNEY_TYPE` to calculate the total journeys for each underground type and year.
   - **Sorting:** The results are sorted by the total number of journeys in ascending order to show the least popular years for the London Underground.
   - **Limit:** Displays the bottom 5 records.

## Usage
1. **Most Popular Transport Types:** Run the `most_popular_transport_types` query to see which transport types have the highest number of journeys in millions.
2. **Emirates Airline Popularity:** Use the `emirates_airline_popularity` query to find the months and years when the Emirates Airline was most popular.
3. **Least Popular Years for the London Underground:** Execute the `least_popular_years_tube` query to identify the least popular years for the London Underground based on the number of journeys.