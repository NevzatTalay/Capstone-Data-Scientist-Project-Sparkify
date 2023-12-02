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
   4. [ Included Libraries](#Included-Libraries)
   5. [How to Run](#how-to-run)

# Spark Churn Analysis Project

## Overview

This repository contains a comprehensive analysis of user interactions within a music application, focusing on predicting user churn using Apache Spark and Python. The project encompasses data exploration, data wrangling, feature engineering, and the implementation of machine learning algorithms.

## Project Structure

### 1. Dataset

- Source: "medium-sparkify-event-data.json"
- Description: Records every user action in the music application.
- Columns:
  -   **artist** - the artist of the soundtrack,
  -   **auth** - variable indicating whether the user has canceled the subscription or not,
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
  -117 users downgraded subscriptions.
  -   15,700 records with no user IDs.
  -   Popular pages: "Next Song," "Home," "Thumbs Up."
  -   User locations: New York, Los Angeles, Boston.
  -   Popular artists: "Kings of Leon," "Coldplay," "Florence."
  -   Listening peak: 15:00-17:00.

### 3. Data Wrangling

- Transformation of registration and timestamp columns into Unix time.
- Removal of rows with no user or session ID. The reason is that users with no userId is just the people visiting webpage with no registration or people are trying to register.
- Creation of a user dataframe for churn activities (churn_matrice).

### 4. Feature Engineering

- Creation of a feature matrix with user IDs and various behavioral metrics.
- Metrics include session count, average session time, song-related actions, and page interactions and many more below:
  -   numof_ses_byuser-Number of Sessions that each user created
  -   session_valid_matrice-Average Session Time spent in App by each session
  -   max_time_spent_per_user - Maximum Spent Time in the App
  -   next_song_by_user - Number of times users trigger next song event.
  -   thumbs_up_by_user - Number of times users click button of thumbs-up
  -   thumbs_down_by_user - Number of times users click button of thumbs-down
  -   merged_df - Ratio of the Thumbs-up and Thumbs-down
  -   downgrade_by_user - Number of times users visit the downgrade page.
  -   error_page_by_user - Number of times users visit the downgrade page.
  -   song_valid - Average songs played in each session.
  -   addfriend_by_user - Number of times users visit the add friend page.
  -   help_by_user - Number of times users visit the help page.
  -   playlist_by_user - Number of times users visit the add to playlist page.
  -   advert_by_user - Number of times users have seen advertisement.

### 5. Machine Learning: Random Forest Classifier

- Features normalized using `Standard Scaler`.
- Training of `Random Forest classifier`.
- Dataset split into training and testing sets.
- Model evaluation based on the F1 score (0.66).

### 6. Machine Learning: Pipeline and GridSearch

- Three pipelines for `logistic regression`, `random forest`, and `gradient-boosted tree classifiers`.
- Feature columns assembled into vectors and standardized.
- Hyperparameter tuning via cross-validation.
- Model performance assessed using the F1 score.
![image](https://github.com/NevzatTalay/Capstone-Data-Scientist-Project-Sparkify/readme_images/1.png)

## Conclusion

This Spark churn analysis project showcases the capabilities of Apache Spark and Python in deciphering complex user datasets and predicting churn. The combination of exploratory data analysis, data wrangling, feature engineering, and advanced machine learning techniques makes this project a comprehensive exploration of Spark's potential in user analytics.

## Included Libraries
```
import ibmos2spark, os
from pyspark.sql import SparkSession
from pyspark.sql.functions import avg, col, concat, desc, explode, lit, min, max, split, udf, from_unixtime, when, sum, count
from pyspark.sql.types import IntegerType
from pyspark.sql import functions as F
from pyspark.sql.functions import min as Fmin, max as Fmax, sum as Fsum, round as Fround
from pyspark.sql import Window
from pyspark.sql.window import Window

from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
from pyspark.ml import Pipeline
from pyspark.ml.feature import VectorAssembler, StandardScaler
from pyspark.ml.evaluation import MulticlassClassificationEvaluator, BinaryClassificationEvaluator     
from pyspark.ml import Pipeline                                                                                      
from pyspark.ml.classification import LogisticRegression, RandomForestClassifier, GBTClassifier                     

import pandas as pd                                                                                                          
from IPython.display import display, HTML                                                                               
import re                                                                                                                     
import datetime                                                                                                         
import numpy as np                                                                                           
import matplotlib.pyplot as plt                                                                                  
%matplotlib inline

```
## How to Run

1. Clone the repository.
2. Install dependencies using `pip install -r requirements.txt`.
3. Open the Jupyter Notebook `Spark_Churn_Analysis.ipynb` in your environment.
4. Execute each cell sequentially for a step-by-step walkthrough.
