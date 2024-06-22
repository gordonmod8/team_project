# Team Project 1

Introduction
We decided to use this dataset from kaggle for our 1st Team project -https://github.com/gordonmod8/team_project/blob/team-project-1/team_project_2.md
The data contains critical features for fraudulent transactions. It contains the following features:

1. distance_from_home
2. distance_from_last_transaction
3. ratio_to_median_purchase_price
4. repeat_retailer
5. used_chip
6. used_pin_number
7. online_order
8. fraud

Exploratory Data Analysis (EDA)

An initial analysis of the dataset was conducted to understand the distribution of features and the extent of class imbalance. We created summary statistics and visualizations to help in identifying patterns and potential correlations between features and the target variable, fraud.

Models Applied

1. Linear Regression
   First, we applied linear regression as a baseline model to understand the relationship between the features and the target variable.
   Although linear regression is not ideal for classification tasks, it provided a simple starting point for model development. We noticed   
   all of the features have very low coefficient value, indicating they have very little influence on the target varible.

2. Multiple Linear Regression with an interaction term

3. K-Nearest Neighbors (KNN)
4. Confusion Matrix
5. Correlatoin Matrix

Addressing Class Imbalance

Upon applying the above models, we realized that the dataset is highly imbalanced with 912,597 non-fraud transactions and only 87,403 fraudulent transactions. We implemented several techniques to mitigate this issue:

- Undersampling method: Undersampling the majority class (non-fraud) to create a balanced dataset
- Random forest:
- Logistic regression:

  




Original Dataset:
Linear Regression
Multiple Reg with interaction term
KNN
 3.  Confusion matrix, accuracy
 4.  Correlation matrix
 5.  Cross validation         - Sarita

Undersample:
Random forest
Confusion matrix
Accuracy
Correlation matrix comparison (higher correlation than the orig)
Logistic regression
Bootstrap, estimation error
Explore what graphs we can display                 - Gordon


Result Summary    - Okky
