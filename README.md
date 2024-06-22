# Team Project 1

## Introduction
We decided to use this dataset from kaggle for our [1st Team project](https://github.com/gordonmod8/team_project/blob/team-project-1/team_project_2.md)
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

## Models Applied

1. Linear Regression
   First, we applied linear regression as a baseline model to understand the relationship between the features and the target variable.
   Although linear regression is not ideal for classification tasks, it provided a simple starting point for model development. We noticed   
   all of the features have very low coefficient value, indicating they have very little influence on the target varible.

2. Multiple Linear Regression with an interaction term
The multiple regression results also had very low coefficients indicating the individual variables had very low correlation but when we modelled the regression for an interaction term between multiple variables, 
the coefficients were significantly higher suggesting that the variables together may have a higher accuracy in predicting fraud.

4. K-Nearest Neighbors (KNN)
The KNN model with K=3 was highly effective with a high accuracy of 99.8%. But High accuracy might be misleading if the dataset is heavily imbalanced.
There is a risk of Minority Class Isolation resulting in a high accuracy.Fraudulent transactions, being rare, might not have enough neighboring instances of the same class. 
This can cause KNN to misclassify them as non-fraudulent because their nearest neighbors are mostly non-fraudulent transactions. Due to limited time, we couldn't try cross validation but that would give us a better understanding of this model.

6. Confusion Matrix
A high number of true negatives (228984) and true positives (21906) show that the model is very effective at identifying both non-fraudulent and fraudulent transactions.
Considering the business implications, missing a fraudulent transaction (false negative) might be more critical than incorrectly flagging a legitimate transaction (false positive).

8. Correlation Matrix
The correlation matrix further strengthened our argument to consider multiple variable interaction to predict fraud.
Also, the coefficients for the sampled data were higher suggesting that a balanced dataset would give us better prediction accuracy.

## Addressing Class Imbalance

Upon applying the above models, we realized that the dataset is highly imbalanced with 912,597 non-fraud transactions and only 87,403 fraudulent transactions. We implemented several techniques to mitigate this issue:

- Undersampling method: Undersampling the majority class (non-fraud) to create a balanced dataset
  
- Random forest: We split the downsampled dataset into training and testing and train a random forest model. The confusion matrix yields a high true positive and true negative results. The accuracy is high at 99.99%. We calculated the ROC AUC Score and the result is high at 99.99%.
  
- Logistic regression:


Confusion matrix

Correlation matrix comparison (higher correlation than the orig)
Logistic regression
Bootstrap, estimation error
Explore what graphs we can display                 - Gordon


## Result Summary
- Okky

Videos of Learning and Experience (Links)
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Sarita : https://drive.google.com/file/d/1J7-f0emnaJabHOkSX0Zo0YLDomFkHgPA/view?usp=drive_link
