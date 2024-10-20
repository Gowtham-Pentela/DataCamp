# Student Data Analysis - SQL Queries

## Overview

This repository contains SQL queries designed to analyze data from the `students` table. The main focus of these queries is to retrieve student records and analyze data related to international students, specifically their stay duration and average scores in three psychological scales (PHQ, SCS, and AS). These insights can help in understanding the well-being of international students based on the duration of their stay.

### Queries

1. **View All Student Data** (`students_data_view`):
   This query retrieves all records from the `students` table, providing a complete overview of the student data.
   
   **Query:**
   ```sql
   SELECT * 
   FROM students;
   ```

   - **Table:** `students`
   - **Columns:** All columns from the `students` table.
   - **Purpose:** To display the full dataset of students for further analysis or exploration.

2. **International Students' Stay and Psychological Scale Analysis** (`intl_students_stay_analysis`):
   This query analyzes international students (`Inter_dom = 'Inter'`) by grouping them based on their length of stay. It calculates the number of students per stay group and computes the average scores for three psychological scales:
   
   - **PHQ (Patient Health Questionnaire)**: Measures depression levels.
   - **SCS (Social Connectedness Scale)**: Measures social connectedness.
   - **AS (Anxiety Scale)**: Measures anxiety levels.
   
   **Query:**
   ```sql
   SELECT stay, 
          COUNT(*) AS count_int, 
          ROUND(AVG(todep), 2) AS average_phq, 
          ROUND(AVG(tosc), 2) AS average_scs, 
          ROUND(AVG(toas), 2) AS average_as
   FROM students
   WHERE Inter_dom = 'Inter'
   GROUP BY stay
   ORDER BY stay DESC;
   ```

   - **Table:** `students`
   - **Columns Returned:**
     - `stay`: The length of stay for the student (e.g., number of years).
     - `count_int`: The number of international students in each stay group.
     - `average_phq`: The average PHQ score (rounded to 2 decimal places) for students in each stay group.
     - `average_scs`: The average SCS score (rounded to 2 decimal places) for students in each stay group.
     - `average_as`: The average AS score (rounded to 2 decimal places) for students in each stay group.
   - **Conditions:** Filters only international students (`Inter_dom = 'Inter'`).
   - **Grouping:** The data is grouped by the `stay` duration.
   - **Sorting:** The results are ordered by `stay` in descending order.

## Usage
1. **View Student Data:** Run the `SELECT * FROM students;` query to retrieve and explore the full dataset.
2. **Analyze International Students:** Use the second query to analyze international students based on their stay duration and psychological scores, allowing for insights into the impact of stay duration on their well-being.