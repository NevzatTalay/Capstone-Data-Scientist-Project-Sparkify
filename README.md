# Table of Contents

1. [Spark Churn Analysis Project](#spark-churn-analysis-project)
   1. [Overview](#overview)
   2. [Project Structure](#project-structure)
      1. [1. Dataset](#1-dataset)
      2. [2. Exploratory Data Analysis (EDA)](#2-exploratory-data-analysis-eda)
      3. [3. Data Wrangling](#3-data-wrangling)
      4. [4. Feature Engineering](#4-feature-engineering)
      5. [5. Machine Learning: Random Forest Classifier](#5-machine-learning-random-forest-classifier)
      6. [6. Machine Learning: Pipeline and GridSearch](#6-machine-learning-pipeline-and-gridsearch)
   3. [Conclusion](#conclusion)
   4. [Dependencies](#dependencies)
   5. [How to Run](#how-to-run)
   6. [Acknowledgments](#acknowledgments)

# Spark Churn Analysis Project

## Overview

This repository contains a comprehensive analysis of user interactions within a music application, focusing on predicting user churn using Apache Spark and Python. The project encompasses data exploration, data wrangling, feature engineering, and the implementation of machine learning algorithms.

## Project Structure

### 1. Dataset

- Source: "medium-sparkify-event-data.json"
- Description: Records every user action in the music application.
- Columns:
  - **artist** - the artist of the soundtrack,
  - **auth** - variable indicating whether the user has canceled the subscription or not,
  -   **firstName** - first name of the user,
  -   **gender** - gender of the user,
  -   **ItemInSession** - Item ID for each session (row) recorded,
  -   **lastName** - last name of the user,
  -   **length** - length of each session by the user,
  -   **level** - the level of subscription of the user (free trial or paid),
  -   **location** - location data of the user (city and state),
  -   **method** - method of access to the page (PUT or GET)
  -   **page** - the page in Sparkify the user visited in each session,
  -   **registration** - user’s registration timestamp,
  -   **sessionId** -  a session id,
  -   **song** - the song listened to in each session, by the user,
  -   **status** - result of the request while accessing,
  -   **ts** - the timestamp of each session,
  -   **userAgent** - the user agent used by the user to visit sparkify,
  -   **userId** - unique number identifying each user.

### 2. Exploratory Data Analysis (EDA)

- Summary:
  - 543,705 rows and 18 columns.
  - Gender distribution: 198 women, 250 men (448 unique users).
  - ...

### 3. Data Wrangling

- Transformation of registration and timestamp columns into Unix time.
- Removal of rows with no user or session ID.
- Creation of a user dataframe for churn activities (churn_matrix).

### 4. Feature Engineering

- Creation of a feature matrix with user IDs and various behavioral metrics.
- Metrics include session count, average session time, song-related actions, and page interactions and many more below:
  - numof_ses_byuser - Number of Sessions that each user created
  - ...

### 5. Machine Learning: Random Forest Classifier

- Features normalized using Standard Scaler.
- Training of Random Forest classifier.
- Dataset split into training and testing sets.
- Model evaluation based on the F1 score (0.69).

### 6. Machine Learning: Pipeline and GridSearch

- Three pipelines for logistic regression, random forest, and gradient-boosted tree classifiers.
- Feature columns assembled into vectors and standardized.
- Hyperparameter tuning via cross-validation.
- Model performance assessed using the F1 score.

## Conclusion

This Spark churn analysis project showcases the capabilities of Apache Spark and Python in deciphering complex user datasets and predicting churn. The combination of exploratory data analysis, data wrangling, feature engineering, and advanced machine learning techniques makes this project a comprehensive exploration of Spark's potential in user analytics.

## Dependencies

- Python 3.x
- Apache Spark
- Jupyter Notebook

## How to Run

1. Clone the repository.
2. Install dependencies using `pip install -r requirements.txt`.
3. Open the Jupyter Notebook `Spark_Churn_Analysis.ipynb` in your environment.
4. Execute each cell sequentially for a step-by-step walkthrough.

## Acknowledgments

- This project was inspired by real-world challenges in user analytics.
- Thanks to the Apache Spark and Python communities for their invaluable contributions.

Feel free to explore, analyze, and extend this project for further insights into user behavior and churn prediction.
