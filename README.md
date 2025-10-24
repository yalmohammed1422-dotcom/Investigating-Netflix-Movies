# Netflix 1990s Movie Analysis

A data analysis project exploring Netflix movie data from the 1990s decade, focusing on movie durations and genre-specific characteristics.

## Overview

This project analyzes Netflix movie data to answer two key questions about films released in the 1990s:
1. What was the most common movie duration in the 1990s?
2. How many short Action movies (under 90 minutes) were released during this decade?

## Features

- **Decade Filtering**: Analyzes movies released between 1990-1999
- **Duration Analysis**: Identifies the most frequently occurring movie duration
- **Genre-Specific Counting**: Counts short Action movies based on duration threshold

## Requirements

1. Load your Netflix dataset into a pandas DataFrame named `netflix_df`
2. Ensure the DataFrame contains the required columns
3. Run the analysis scripts to get insights
```python
# Importing pandas and matplotlib
import pandas as pd
import matplotlib.pyplot as plt

# Read in the Netflix CSV as a DataFrame
netflix_df = pd.read_csv("netflix_data.csv", index_col=0)
```

## Dataset

The analysis expects a DataFrame named `netflix_df` with the following columns:
- `release_year`: Year the movie was released
- `type`: Content type (Movie or TV Show)
- `duration`: Length of the movie in minutes
- `genre`: Movie genre/category

## Code Structure

### Analysis 1: Most Common Movie Duration in the 1990s

```python
# Filter for movies released before 2000
decade = netflix_df[(netflix_df["release_year"] < 2000)&(netflix_df["type"] == "Movie")]

# Count frequency of each duration
decade["freq"] = decade["duration"].map(decade["duration"].value_counts())

# Find the maximum frequency
max_freq = decade["freq"].max()

# Get duration(s) with maximum frequency
duration_df = decade[decade["freq"] == max_freq]

# Select the highest duration if multiple durations have the same frequency
duration = duration_df["duration"].max()
```

**Logic**: This code identifies the most frequently occurring movie duration in the 1990s. If multiple durations have the same frequency, it returns the longest one.

### Analysis 2: Count of Short Action Movies

```python
# Initialize counter
short_movie_count = 0

# Filter for 1990s decade
decade1 = netflix_df[(netflix_df["release_year"] < 2000)&(netflix_df["release_year"] >= 1990)]

# Filter for Action movies only
decade1 = decade1.loc[(decade1["type"] == "Movie") & (decade1["genre"] == "Action")]

# Count movies with duration less than 90 minutes
short_movie_count = len(decade1[decade1["duration"] < 90])
```

**Logic**: This code counts how many Action movies from the 1990s have a duration of less than 90 minutes.


## Results

The analysis provides:
- **Most Common Duration**: The most frequently occurring movie duration in 1990s movies: 94
- **Short Action Movie Count**: Total number of Action movies under 90 minutes from the 1990s: 7

## Visualization
<img width="2382" height="1179" alt="image" src="https://github.com/user-attachments/assets/ccac507f-d687-4c1f-adb7-a37f5c9b9a02" />
<img width="2382" height="1181" alt="image" src="https://github.com/user-attachments/assets/6407d731-be5a-4f2e-97e5-c50f95f66649" />

## Author

Yousef Almohammed - Netflix Data Analysis Project

---

*This analysis is part of a data exploration project on Netflix content trends.*
