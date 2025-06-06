# movie-insights
Exploring movie data with Python — from insights to recommendations

## Project Background
In the film industry, making sense of large volumes of movie data is key to understanding what drives audience interest and box office success. With thousands of movies spanning decades, structured analysis can uncover hidden patterns and improve decision-making for studios, streaming platforms, and viewers alike.

This project leverages [The Movies Dataset](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset/data?status=pending&select=movies_metadata.csv) from Kaggle to explore the landscape of film production and reception through data-driven methods. It combines exploratory analysis with several recommendation systems to uncover trends and generate personalized movie suggestions, highlighting the practical value of data science in the creative industry.

## Project Goal
This project aims to analyze movie metadata using **Python Jupyter Notebook** to uncover patterns in film performance and audience preferences. It further develops and compares multiple types of recommendation systems to generate personalized movie suggestions based on different modeling approaches.

## Table of Contents
- README.md
- LICENSE.txt
- movies_cleaned.csv
- data cleaning.ipynb
- recommendation_algorithm.ipynb

## Instructions

### 1. Package Used

### 2. Dataset Used
This project uses [The Movies Dataset](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset/data?status=pending&select=movies_metadata.csv) from Kaggle, which contains metadata for over 45,000 movies, including information on genres, cast, crew, release dates, budgets, revenues, and user ratings. Additional files such as ratings and credits support deeper analysis and the development of various recommendation models.

Due to their large file sizes, the following datasets are not included in the GitHub repository:
- links_small.csv
- links.csv
- credits.csv
- movies_metadata.csv
- ratings.csv
- ratings_small.csv
- keywords.csv

The `data cleaning.ipynb` notebook generates a cleaned version of the movie dataset, saved as `movies_cleaned.csv`. This file serves as a standardized and preprocessed dataset for use in subsequent analysis and model development.

## License
This project is licensed under the MIT License - see the [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/leopengningchuan/movie-insights?tab=MIT-1-ov-file) file for details.
