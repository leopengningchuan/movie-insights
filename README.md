# movie-insights
Exploring movie data with Python — from insights to recommendations

## Table of Contents
- [Project Background](#project-background)
- [Project Goal](#project-goal)
- [File Structure](#file-structure)
- [Instructions](#instructions)
  - [1. Packages Used](#1-packages-used)
  - [2. Datasets Used](#2-datasets-used)
  - [3. Data Cleaning](#3-data-cleaning)
    - [3.1 movies_metadata](#31-movies_metadata)
    - [3.2 ratings_small & ratings](#32-ratings_small--ratings)
  - [4. Exploratory Data Analysis](#4-exploratory-data-analysis)
  - [5. Recommendation Algorithms](#5-recommendation-algorithms)
    - [5.1 Top Weighted Rating Recommendation](#51-top-weighted-rating-recommendation)
    - [5.2 Recommendation by Favorite Genre](#52-recommendation-by-favorite-genre)
    - [5.3 Collaborative Filtering](#53-collaborative-filtering)
- [Future Improvements](#future-improvements)
- [License](#license)

## Project Background
In the film industry, making sense of large volumes of movie data is key to understanding what drives audience interest and box office success. With thousands of movies spanning decades, structured analysis can uncover hidden patterns and improve decision-making for studios, streaming platforms, and viewers alike.

This project leverages [*The Movies Dataset*](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset/data?status=pending&select=movies_metadata.csv) from Kaggle to explore the landscape of film production and reception through data-driven methods. It combines exploratory analysis with several recommendation systems to uncover trends and generate personalized movie suggestions, highlighting the practical value of data science in the creative industry.

## Project Goal
This project aims to analyze movie metadata using **Python Jupyter Notebook** to uncover patterns in film performance and audience preferences. It further develops and compares multiple types of recommendation systems to generate personalized movie suggestions based on different modeling approaches.

## File Structure

Configuration & Metadata:
- `README.md` – project overview
- `LICENSE.txt` – license information
- `.gitignore` – git ignore config
- `.gitattributes` – git attributes config

Core Logic:
- `data_cleaning.ipynb` – notebook for data cleaning
- `exploratory_data_analysis.ipynb` – notebook for exploratory data analysis
- `recommendation_algorithm.ipynb` – notebook for recommendation algorithm
- `original_data/` – directory containing raw data files from the original Kaggle dataset
  - `movies_metadata.csv` – raw movie metadata
  - `credits.csv` – raw cast and crew information
  - `keywords.csv` – raw keywords associated with each movie
  - `links.csv` – mapping between TMDb and IMDb IDs
  - `links_small.csv` – smaller version of the `links.csv` file
  - `ratings.csv` – full user rating dataset
  - `ratings_small.csv` – sample of the full ratings dataset
- `cleaned_data/` – folder containing processed datasets
  - `movies_cleaned.csv` – cleaned movie metadata
  - `movie_metadata_supporting.xlsx` – extracted lookup tables from structured fields
  - `ratings_small_cleaned.csv` – cleaned subset of user ratings

## Instructions

### 1. Packages Used
- `pandas`, `datetime`, `numpy`, `itertools`: for data manipulation
- `os`: for file path handling
- `ast`: for processing abstract syntax grammar
- `matplotlib`: for data visualization
- `sklearn`: for modeling

### 2. Datasets Used
This project uses [*The Movies Dataset*](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset/data?status=pending&select=movies_metadata.csv) from Kaggle, which contains metadata for over 45,000 movies, including information on genres, release dates, budgets, revenues, and user ratings. Additional files such as ratings and credits support deeper analysis and the development of various recommendation models.

Both raw and cleaned versions of the data are included in the repository under the `original_data/` and `cleaned_data/` directories, respectively. For detailed file listings and descriptions, see the [File Structure](#file-structure) section.

### 3. Data Cleaning
To ensure consistency and usability, raw datasets were cleaned and standardized before analysis and modeling. This included type conversion, missing value handling, metadata merging, and structured field parsing across multiple files.

#### 3.1 movies_metadata
The `movies_metadata` dataset is cleaned and enriched using the `keywords` and `credits` datasets to prepare for further use:
- Performed general data cleaning on fields such as `id`, `budget`, `popularity`, and `release_date`, including type conversions and removal of invalid rows.
- Merged additional metadata (e.g. `keywords`, `cast`, and `crew`) from the `keywords` and `credits` datasets based on movie `id`.
- Parsed structured string fields (e.g. `genres`, `cast`, `crew`, `keywords`, etc.) into native Python lists and dictionaries.
- Simplified list/dictionary fields by retaining only the `id`, and saved the supporting metadata to `movie_metadata_supporting.xlsx`.
- Renamed columns for clarity and removed irrelevant or redundant columns to streamline the dataset for downstream use.
- Saved the cleaned dataset to `movies_cleaned.csv`.

#### 3.2 ratings_small & ratings
The `ratings_small` and `ratings` datasets are cleaned and enriched using the `links` datasets to prepare for further use:
- Converted `timestamp` fields into readable datetime format and stored as `date_time`.
- Mapped `movieId` to `imdb_id` using the `links` dataset for compatibility with external metadata.
- Renamed columns for clarity and removed irrelevant or redundant columns to streamline the dataset for downstream use.
- Saved the cleaned dataset to `ratings_small_cleaned.csv` and `ratings_cleaned.csv`.

### 4. Exploratory Data Analysis
Exploratory Data Analysis (EDA) was conducted on the `movies_cleaned` dataset to uncover patterns in movie production and audience reception:
- Relationship between genre and average vote rating  
- Trends in movie count and vote count over release years  
- Trends in average vote rating over release years  

### 5. Recommendation Algorithm
Several recommendation strategies were implemented to suggest movies based on user preferences and content features.

#### 5.1 Top Weighted Rating Recommendation
To highlight high-quality movies with sufficient audience engagement, a weighted rating formula was used to rank movies more fairly:

**weighted_rating = (v × R + m × C) / (v + m)**

Where:
- **R**: average rating of the movie  
- **v**: number of votes for the movie  
- **m**: number of votes threshold for qualified movies
- **C**: mean rating across all movies

Movies with vote counts above the threshold (using 75th percentile in this case) were considered "qualified" for ranking. The final `weighted_rating` was computed for each, and the top 20 were selected as overall recommendations. In addition, the top 10 highest weighted rating movies were identified within each genre to support genre-based browsing.

#### 5.2 Recommendation by Favorite Genre
This method generates personalized recommendations by identifying the genres most preferred by a given user. The process begins by retrieving all movies the user has rated and selecting those with the highest scores. Based on the genre indicators of these top-rated movies, the user's favorite genres are inferred.

Once the preferred genres are determined, the system filters out movies the user has already seen and searches the remaining qualified movies for those belonging to the same genres. These candidate movies are then ranked by their weighted rating score to ensure quality and popularity. The final result is a list of top recommendations that match the user's taste profile while maintaining high content quality.

#### 5.3 Collaborative Filtering
This approach leverages user-to-user collaborative filtering to generate personalized movie recommendations based on rating patterns. A user–item rating matrix was constructed from the `ratings_small_cleaned` dataset, with missing values filled as zeros for similarity computation. Cosine similarity was then used to calculate the similarity between users.

For a target user, the top 10 most similar users were identified. Their ratings were aggregated using a similarity-weighted average to estimate the target user's potential interest in unseen movies. Movies already rated by the user were excluded, and the top-scoring titles—ranked by both weighted score and average similarity—were selected as recommendations.

This method is effective for capturing nuanced user preferences based on community behavior, particularly when overlapping movie ratings exist between users.

## Future Improvements
- **Content-Based Movie Recommendation**: Implement a content recommendation algorithm to suggest movies with similar attributes (e.g., genre, cast, keywords).
- **Popularity‐Adjusted Recommendation**: Blend personalized suggestions with popularity to balance novelty and relevance.

## License
This project is licensed under the MIT License - see the [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/leopengningchuan/movie-insights?tab=MIT-1-ov-file) file for details.

## Acknowledgements
- Thanks to [Kaggle](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset) and the original dataset contributor [Rounak Banik](https://www.kaggle.com/rounakbanik) for providing *The Movies Dataset*.
