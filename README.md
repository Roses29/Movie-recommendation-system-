🌍 [Lire en Français](README_FR.md) | 📓 [See PDF](./RobinRubangura_Recommendation_Systems.ipynb)
)

# 🎬 Movie Recommendation System

## Overview

This project builds a **Movie Recommendation System** inspired by platforms like Netflix. Using a dataset of user-movie ratings, three distinct recommendation approaches are implemented and compared, ranging from simple popularity-based methods to advanced matrix factorization techniques.

## Dataset

The `ratings.csv` dataset contains **100,004 interactions** across **671 unique users** and **9,066 unique movies**, with the following columns:

- `userId` – unique user identifier
- `movieId` – unique movie identifier
- `rating` – score given by the user (scale 0–5)
- `timestamp` – dropped as not needed for analysis

**Key observations:** ratings of 4 are the most frequent; the distribution of user interactions is right-skewed, meaning most users rate relatively few movies.

## Models Built

#### 1. 🏆 Rank-Based Recommendation System
Recommends the most popular movies based on average rating, with a configurable minimum interaction threshold. Used to handle **cold-start problems** (new users with no history).

#### 2. 👥 User-User Similarity-Based Collaborative Filtering (KNN)
Finds users with similar tastes and recommends movies they liked. Uses **cosine similarity** and **KNN**, tuned via GridSearchCV.

| | Baseline | Tuned |
|---|---|---|
| RMSE | 0.9925 | 0.9871 |

#### 3. 🎞️ Item-Item Similarity-Based Collaborative Filtering (KNN)
Recommends movies similar to those a user has already rated highly. Tuning significantly improved results.

| | Baseline | Tuned |
|---|---|---|
| RMSE | 1.0032 | 0.9495 |

#### 4. 🧮 Matrix Factorization – SVD (Singular Value Decomposition)
Decomposes the user-item matrix into latent factors, capturing hidden patterns. Best overall performance.

| | Baseline | Tuned |
|---|---|---|
| RMSE | 0.9054 | 0.8953 |

## Model Comparison (Precision & Recall @ k=5 and k=10)

SVD achieves the best RMSE overall. After tuning, the item-item model surpasses user-user in RMSE (0.9495 vs 0.9871). Precision and recall values are comparable across tuned models, with SVD competitive with user-user similarity.

## Key Takeaways

- **SVD outperforms** KNN-based methods in RMSE thanks to latent feature extraction and better handling of sparse data.
- **Hyperparameter tuning** has a stronger impact on item-based models than user-based ones.
- **A/B Testing** is recommended to measure real-world effectiveness of any deployed model.

## Tech Stack

- **Python** – pandas, NumPy, Matplotlib, Seaborn
- **Surprise** – KNNBasic, SVD, GridSearchCV, KFold, precision_recall_at_k

