# Music Recommendation System

A capstone project completed as part of the [Applied AI and Data Science Program](https://professional.mit.edu/course-catalog/applied-ai-and-data-science-program) from MIT Professional Education — a 14-week certificate program covering machine learning, recommendation systems, deep learning, and generative AI, developed and taught by MIT faculty.

The project builds and evaluates a music recommendation engine using the Million Song Dataset. The system predicts the top 10 tracks a given user is most likely to enjoy based on their listening history.

## Problem

Digital music platforms depend on surfacing relevant content to keep listeners engaged. This project frames the challenge as a matrix completion and ranking problem: given a sparse user-song interaction matrix built from play counts, predict preference scores for unheard tracks and return the highest-ranked results.

## Data

The project uses the [Taste Profile Subset](http://millionsongdataset.com/) from the Million Song Dataset, which provides two files:

- **song_data** — song metadata: title, album, artist, and year of release
- **count_data** — implicit feedback: user ID, song ID, and play count

The raw dataset contains roughly two million user-song interactions and one million song records. After filtering for minimum listener activity and song interaction thresholds, the working dataset is reduced to 138,301 rows covering 3,337 users, 620 songs, and 247 artists.

> **Note:** The data files are not included in this repository — they were sourced from proprietary course material and exceed GitHub's file size limits. The equivalent public source is the [Million Song Dataset](http://millionsongdataset.com/) and its associated [Taste Profile Subset](http://millionsongdataset.com/tasteprofile/).

## Approach

Two recommendation strategies are implemented and compared:

**Popularity-based filtering** ranks songs by aggregate or average play count across all users. It serves as a non-personalized baseline and is sensitive to the minimum play count threshold chosen.

**Collaborative filtering (user-user similarity)** uses the `surprise` library to identify users with similar listening patterns and recommend songs those users enjoyed. Play count acts as a proxy for implicit preference. Models are evaluated on Precision@K, Recall@K, RMSE, and F1@K.

## Key Findings

- A baseline KNNBasic user-user model achieved Precision@K of 0.40 and Recall@K of 0.71 before tuning.
- Hyperparameter tuning produced marginal gains, suggesting the model has reached its performance ceiling on this dataset.
- Nearly 48% of songs have no valid release year, so year is excluded as a model feature and retained only as optional post-retrieval metadata.
- Popularity-based recommendations are highly sensitive to the aggregation method chosen (sum vs. mean play count) and the minimum interaction threshold applied.

## Repository Contents

| File | Description |
|------|-------------|
| [music_recommender.ipynb](music_recommender.ipynb) | Full analysis: data preparation, EDA, model training, evaluation, and recommendations |
| [music_recommender.pdf](music_recommender.pdf) | Presentation summarizing the problem, methodology, and results |
