# Team Project 1

## Abstract
Global losses in credit card fraud have risen from over USD 18 B in 2014 to over USD 33 B in 2024 [(Statista)](https://www.statista.com/statistics/1394119/global-card-fraud-losses/). The timely detection of fraud and application of interventions can attenuate the damage of this category of crime. There are many statistical models available to apply to this problem and each will yield a different accuracy. In order to aid in model selection we investigate the accuracy of several supervised training models in predicting fraud. 

## Introduction
Before forming our team we each filled out a survey of our research interests. Because of our shared interest in the Finance sector and machine learning techniques the four of us were selected to form Group 2. We searched for datasets that were highly rated for being well maintained and we filtered for financial focused data. We ultimately decided to use the [*"Credit Card Fraud"* dataset by Dhanush Narayanan R, accessed on Kaggle](https://www.kaggle.com/datasets/dhanushnarayananr/credit-card-fraud) for our [1st Team project](https://github.com/gordonmod8/team_project/blob/team-project-1/team_project_2.md).
The data in this repository comes in a csv file and has a million rows, with critical features for fraudulent transactions and a response variable True/False for fraud. It contains the following features:


1. distance_from_home
2. distance_from_last_transaction
3. ratio_to_median_purchase_price
4. repeat_retailer
5. used_chip
6. used_pin_number
7. online_order
8. fraud


Nearly universally folks have experience with these predictors and credit card security incidents. Hence these predictors were particularly compelling to study. 

## Rules of Engagement

The Group 2 team has four members: Sarita Rana, Elizabeth Yeo, Okky Rijanto, and Gordon Geringas. The analysis efforts were divided by statistical model and assigned to each team member. Initially the analysis was to be committed on Github in a single notebook. But the tasks of diffing and merging the ipynb format was not a good match on Github. With a limited time budget for troubleshooting spent, the team resolved to split the analysis into multiple workbooks in the /src folder.


The scope of analysis techniques was reduced so as to apply just the techniques of our previous module in the Data Sciences Institute Certificate, "Applying Statistical Concepts". In the prior 3 weeks we studied Multivariable Regression, Logistic Regression, K-Nearest-Neighbours, Confusion Matrix and Correlation Matrix, Cross-Validation and Bootstrapping from the source [*"Introduction to Statistical Learning with Applications in Python"* by James, Witten, Hastie, Tibshirani and Taylor](https://www.statlearning.com/). 


Our agendas at each meeting advanced the project's required deliverables. The first meeting initialized our repository and selected a data set of common interest. The second meeting divided the analysis by team members. The third meeting attempted merges and solved data analysis problems. The fourth meeting consolidated the findings and assigned the README efforts. The fifth meeting was editorial.


Agreement on team decisions was found through a quorum of a majority of members present in the calls which took place in Breakout Rooms on Zoom. A record of those team decisions and assigned deliverables was kept in Slack DMs. The low amount formality was optimal since the team was a self-accountable unit. Project management solutions such as Jira or Trello were considered but ultimately rejected due to the lack of applicability of their features to the project's limited complexity, and duration.


## Exploratory Data Analysis (EDA)


An initial analysis of the dataset was conducted to understand the distribution of features and the extent of class imbalance. We created summary statistics and visualizations to help in identifying patterns and potential correlations between features and the target variable, fraud.


## Models Applied


1. Linear Regression
  First, we applied linear regression as a baseline model to understand the relationship between the features and the target variable.
  Although linear regression is not ideal for classification tasks, it provided a simple starting point for model development. We noticed  
  all of the features have very low coefficient value, indicating they have very little influence on the target variable.


2. Multiple Linear Regression with an interaction term
The multiple regression results also had very low coefficients indicating the individual variables had very low correlation but when we modeled the regression for an interaction term between multiple variables,
the coefficients were significantly higher suggesting that the variables together may have a higher accuracy in predicting fraud.


4. K-Nearest Neighbors (KNN)
The KNN model with K=3 was highly effective with a high accuracy of 99.8%. But High accuracy might be misleading if the dataset is heavily imbalanced.
There is a risk of Minority Class Isolation resulting in a high accuracy.Fraudulent transactions, being rare, might not have enough neighboring instances of the same class.
This can cause KNN to misclassify them as non-fraudulent because their nearest neighbors are mostly non-fraudulent transactions. Due to limited time, we couldn't try cross validation but that would give us a better understanding of this model.


6. Confusion Matrix
A high number of true negatives (228984) and true positives (21906) show that the model is very effective at identifying both non-fraudulent and fraudulent transactions.
Considering the business implications, missing a fraudulent transaction (false negative) might be more critical than incorrectly flagging a legitimate transaction (false positive).


8. Correlation Matrix
The correlation matrix further strengthened our argument to consider multiple variable interactions to predict fraud.
Also, the coefficients for the sampled data were higher suggesting that a balanced dataset would give us better prediction accuracy.


## Addressing Class Imbalance


Upon applying the above models, we realized that the dataset is highly imbalanced with 912,597 non-fraud transactions and only 87,403 fraudulent transactions. We implemented several techniques to mitigate this issue:


- Undersampling method: Undersampling the majority class (non-fraud) to create a balanced dataset
 - Random forest: We split the downsampled dataset into training and testing and train a random forest model. The confusion matrix yields high true positive and true negative results. The accuracy is high at 99.99%. We calculated the ROC AUC Score and the result is high at 99.99%.
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


Elizabeth Yeo : https://drive.google.com/file/d/16CQnj9jih-SSa84uT4QGoKti-7Boy8Pe/view?usp=drive_link


