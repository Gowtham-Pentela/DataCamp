# Netflix Data Analysis - Python Script

## Overview

This Python script analyzes Netflix data, focusing on movies released in the 1990s. The script uses pandas for data manipulation and Matplotlib for visualization, with the goal of filtering and analyzing movies based on specific conditions such as release year, genre, and duration.

### Script Details

1. **Importing Libraries**:
   - The script imports essential libraries for data analysis and visualization:
     - `pandas`: For reading and manipulating the Netflix dataset.
     - `matplotlib.pyplot`: For potential visualizations (though none are used directly in the current code).

   **Code:**
   ```python
   import pandas as pd
   import matplotlib.pyplot as plt
   ```

2. **Reading Netflix Data**:
   - The script reads a CSV file containing Netflix data (`netflix_data.csv`) into a pandas DataFrame (`netflix_df`).

   **Code:**
   ```python
   netflix_df = pd.read_csv("netflix_data.csv")
   ```

3. **Displaying Initial Data**:
   - The `head()` function is used to display the first few rows of the Netflix DataFrame for an initial overview of the dataset.

   **Code:**
   ```python
   netflix_df.head()
   ```

4. **Filtering 1990s Movies**:
   - The script filters the dataset to focus on movies released between 1990 and 1999. The filtered data includes only records where the `type` is "Movie".
   
   **Code:**
   ```python
   filtered_df = netflix_df[(netflix_df['release_year'] >= 1990) & (netflix_df['release_year'] <= 1999) & (netflix_df['type'] == 'Movie')]
   ```

5. **Analyzing Movie Duration**:
   - The script counts the occurrences of different movie durations in the filtered dataset using the `value_counts()` function.
   - It sets a `duration` variable to 94 (though this value is not used further in the current script).

   **Code:**
   ```python
   filtered_df['duration'].value_counts()
   duration = 94
   ```

6. **Filtering Action Movies Under 90 Minutes**:
   - The script further filters the dataset to select only "Action" movies with a duration of less than 90 minutes.
   - It calculates the total number of such short action movies using the `len()` function and stores the count in the `short_movie_count` variable.

   **Code:**
   ```python
   action_movies_under_90 = filtered_df[(filtered_df['genre'] == 'Action') & (filtered_df['duration'] < 90)]
   short_movie_count = len(action_movies_under_90)
   ```

7. **Displaying Short Movie Count**:
   - Finally, the script prints the total number of short action movies under 90 minutes.

   **Code:**
   ```python
   short_movie_count
   ```

### Requirements
- **Dataset**: A CSV file named `netflix_data.csv` containing Netflix data with columns like:
  - `release_year`: Year the movie was released.
  - `type`: Type of content (e.g., "Movie").
  - `duration`: Duration of the movie in minutes.
  - `genre`: Genre of the movie (e.g., "Action").

- **Libraries**: Ensure the following Python libraries are installed:
  - `pandas`
  - `matplotlib`

### Usage
1. Place the `netflix_data.csv` file in the same directory as the script.
2. Run the script to:
   - View an overview of the dataset.
   - Filter and analyze movies released in the 1990s.
   - Determine the count of short action movies under 90 minutes in duration.