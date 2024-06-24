# Predicting Credit Card Fraud: 
## *A Comparison of Supervised Learning Models*
### UofT-DSI — Team Project 1 
### Group 2 — Sarita Rana, Elizabeth Yeo, Okky Rijanto, and Gordon Geringas


## Abstract
Global losses in credit card fraud have risen from over USD 18 B in 2014 to over USD 33 B in 2024 [(Statista)](https://www.statista.com/statistics/1394119/global-card-fraud-losses/). The timely detection of fraud and the application of interventions can help credit institutions attenuate impact of these crimes on a massive scale. There are many statistical models that could predict fraud from transaction data and each will yield a different accuracy. In order to aid in model selection we investigate the accuracy of several supervised learning models in predicting fraud.


## Introduction
Before forming our team we each filled out a survey of our research interests. Because of our shared interest in the Finance sector and machine learning techniques the four of us were selected to form Group 2. We searched for datasets that were highly rated for being well maintained and we filtered for financial focused data. We ultimately decided to use the [*"Credit Card Fraud"* dataset by Dhanush Narayanan R, accessed on Kaggle](https://www.kaggle.com/datasets/dhanushnarayananr/credit-card-fraud) for our [1st Team project](https://github.com/gordonmod8/team_project/blob/team-project-1/team_project_2.md). The data in this repository comes in a csv file and has a million rows. The dataset has 7 critical features for predicting fraudulent transactions and a boolean response for fraud listed:
1. distance_from_home
2. distance_from_last_transaction
3. ratio_to_median_purchase_price
4. repeat_retailer
5. used_chip
6. used_pin_number
7. online_order
8. fraud


Nearly universally folks have had personal experience with each of these predictors and credit card security incidents. Hence, these predictors were particularly compelling to study. We aim to use this data to quantify and compare the predictions of simple statistical learning models on all the available predictors. This kind of improvement in prediction precision will attenuate the financial impact of credit card fraud by locking more criminals out after the first suspicious transaction as well as reduce unnecessary service interruptions by lowering the rate of false positives. The credit institution will be able to better serve its customers and write off fewer losses.


## Rules of Engagement


The Group 2 team has four members: Sarita Rana, Elizabeth Yeo, Okky Rijanto, and Gordon Geringas. The analysis efforts were divided by statistical model and assigned to each team member. Initially each analysis was to be pushed to Github in a single notebook. But the tasks of diffing and merging the ipynb format was not a good match for Github's workflow. With a limited time budget for troubleshooting spent, the team resolved to split the analysis into multiple workbooks in the /src folder.


The scope of analysis techniques was reduced so as to apply just the techniques of our previous module in the Data Sciences Institute Certificate, "Applying Statistical Concepts". In the prior 3 weeks we studied Multivariable Regression, Logistic Regression, K-Nearest-Neighbours, Confusion Matrix and Correlation Matrix, Cross-Validation and Bootstrapping from the source [*"Introduction to Statistical Learning with Applications in Python"* by James, Witten, Hastie, Tibshirani and Taylor; published by Springer](https://www.statlearning.com/).


Our agendas at each meeting advanced the project's required deliverables. The first meeting initialized our repository and selected a data set of common interest. The second meeting divided the analysis by team members. The third meeting attempted merges and solved data analysis problems. The fourth meeting consolidated the findings and assigned the README efforts. The fifth meeting was editorial.


Agreement on team decisions was determined by a consensus of a quorum present in the Breakout Rooms on Zoom. A record of those team decisions and assigned deliverables was kept in Slack DMs. The low amount of formality was optimal since the team was a self-accountable unit. Project management solutions such as Jira or Trello were considered but ultimately rejected due to the lack of applicability of their features to the project's limited complexity, and duration.


## Models, Observations, and Challenges
1. **Exploratory Data Analysis (EDA)**  An initial analysis of the dataset was conducted to understand the cross-correlations and distributions of features and the extent of imbalance of the response. Summary statistics were calculated and with visualizations they helped suggest relationships between features and the target variable, fraud.
2. **Linear Regression**  We applied linear regression as a baseline model to understand the relationship between the features and the target variable. Although linear regression is not ideal for classification tasks, it provided a simple starting point for model development. We noticed all of the features have very low coefficient value, indicating they have very little influence on the target variable.
3. **Multiple Linear Regression with an interaction term**  The multiple regression results also had very low coefficients indicating the individual variables had very low correlation but when we modeled the regression for an interaction term between multiple variables, the coefficients were significantly higher suggesting that the variables together may have a higher accuracy in predicting fraud.
4. **K-Nearest Neighbors (KNN)**  The KNN model with K=3 was highly effective with a high accuracy of 99.8%. But High accuracy might be misleading if the dataset is heavily imbalanced. There is a risk of Minority Class Isolation resulting in a high accuracy. Fraudulent transactions, being rare, might not have enough neighboring instances of the same class. This can cause KNN to misclassify them as non-fraudulent because their nearest neighbors are mostly non-fraudulent transactions. In order to address imbalance, downsampling was investigated.
5. **Downsampling & Correlation Matrix Comparison**  Downsampling was employed to keep all of the positive fraud examples while randomly selecting variables from the rest of the data such that the resulting data frame was 50% fraud and 50% no fraud. The correlation matrix of the dataframe was compared with the initial exploratory data analysis. The coefficients of correlation showed significant gain across the board in the downsampled Data Frame. We predicted that training further learning models on downsampled data could improve the signal of fraud. We expected either improved precision, or we expected the rate of false positives to increase with the rate of false negatives decreased thus improving the attenuation of damages while incurring a lift in service interruptions.
6. **Notebook Merging Workflow Disruptions**  At this stage significant troubleshooting time was spent trying to merge our analysis work into one notebook. Although everyone wrote and resolved pull requests, the merges often corrupted the ipynb file and had to be pushed again which did not require merging since a corrupted file and legitimate file are not merged, simply the legitimate files overwrites the corrupted file. This double PR situation was resolved by accepting multiple ipynbs into the src folder which were pulled in from their respective branches.
7. **Logistic Regression**  The downsampled dataset was exported to a .csv and then loaded into a dataframe. The data was used to train a Logistic Regression learning model which was evaluated for precision and with a confusion matrix. The logistic regression was fairly good at predicting credit card fraud but had a bump in both false-negatives and false positives in comparison with KNN K=3 without downsampling.
8. **Random Forest**  The data was downsampled and a random forest model was trained. The performance of the model was evaluated against test data in the downsampled dataframe using [Area Under the Receiver Operating Characteristic](https://www.geeksforgeeks.org/auc-roc-curve/). This demonstrated an incredible bump in precision. In addition the confusion matrix displayed a significant reduction in both false positives and false negatives.


## Results and Conclusions

Multi-variate Regression Model Results

R-squared (0.284): This means the model explains about 28.4% of the variation in fraud cases. While it captures some key factors influencing fraud, 71.6% of the variation is still unexplained, suggesting that other important factors are not included in the model.
F-statistic (26450.00) and Prob (F-statistic: 0.00): The high F-statistic and the p-value of 0.00 show that the model is statistically significant and the variables included are collectively a good fit for explaining fraud.

Significant Variables
Intercept (-0.0297): The negative intercept suggests a baseline probability of fraud when all other variables are zero. However, this value needs to be interpreted in the context of other variables.
distance_from_last_transaction (0.0021): A positive coefficient here means that as the distance from the last transaction increases, the likelihood of fraud also increases. This is highly significant, with a t-value of 116.152.
ratio_to_median_purchase_price (0.0484): A higher ratio of the transaction amount to the median purchase price is strongly linked to a higher likelihood of fraud.
distance_from_home (0.0013): Similar to the distance from the last transaction, a greater distance from home is associated with a higher probability of fraud.
used_chip (0.0101): Transactions using the chip show a slight increase in fraud probability, possibly reflecting sophisticated fraud tactics targeting chip transactions.

Interaction Effects
distance_from_last_transaction * ratio_to_median_purchase_price (-7.665e-05): This negative interaction suggests that the combined effect of these factors slightly decreases the probability of fraud.
distance_from_last_transaction * distance_from_home (-1.901e-06): This negative interaction indicates that the combined influence of these two distances slightly reduces the likelihood of fraud.
ratio_to_median_purchase_price * distance_from_home (-5.945e-05): This negative interaction effect shows that a high ratio to the median purchase price combined with a long distance from home slightly decreases fraud probability.
distance_from_last_transaction * ratio_to_median_purchase_price * distance_from_home (6.486e-07): This small positive interaction indicates a slight increase in the probability of fraud when these three factors are combined.
distance_from_last_transaction * used_chip (-0.0021) and ratio_to_median_purchase_price * used_chip (-0.0043): Both interactions have a negative impact, suggesting that using a chip reduces the likelihood of fraud for transactions far from the last transaction and with a high ratio to median purchase price.

Logistics Regression Results
Log-Likelihood: The model's Log-Likelihood is -36594, compared to the null model's -121170. This significant improvement shows that the model effectively captures important factors influencing fraud.
Pseudo R-squared (0.6980): About 69.8% of the variation in fraud is explained by the model, indicating a good fit.
LLR p-value (0.000): The model is statistically significant overall

Significant Variables
Intercept (-7.7086): This negative value indicates a very low baseline probability of fraud when all other variables are zero.
Distance from Home (0.0290): As the distance from home increases, so does the likelihood of fraud. This variable is highly significant (z-value: 130.628).
Distance from Last Transaction (0.0514): A greater distance from the last transaction also correlates with a higher probability of fraud (z-value: 88.346).
Ratio to Median Purchase Price (1.2289): Transactions that are much higher than the median purchase price strongly indicate fraud (z-value: 180.881).
Repeat Retailer (-1.4494): Transactions with repeat retailers are less likely to be fraudulent, shown by the negative coefficient and significant z-value of -45.752.
Used Chip (-1.2277): Using a chip decreases the likelihood of fraud (z-value: -53.908).
Used PIN Number (-10.2523): Transactions using a PIN number are much less likely to be fraudulent, with a very significant negative coefficient (z-value: -63.503).
Online Order (5.0528): Online orders have a much higher probability of being fraudulent, as indicated by the large positive coefficient (z-value: 117.244).

Comparison between Multivariate (original sample) and Logistics (undersampled)
•	Fit and Variability: Logistic regression explains a much larger portion of the variability in fraud (69.8%) compared to the multi-variate regression (28.4%).
•	Significance: Both models are statistically significant overall.
•	Strength of Relationships: Logistic regression generally shows stronger relationships between predictors and the likelihood of fraud, as indicated by the larger coefficients.
•	Direction of Effects: Both models agree on the direction of most effects (e.g., distance from last transaction, ratio to median purchase price), but they differ significantly on the effect of using a chip.


Classification Methods Results

KNN

| Model         | Precision | False Negative Rate | False Positive Rate |
|---------------|-----------|---------------------|---------------------|
| KNN           | 0.9947    | 0.0088              | 0.0005              |
| RndFor        | 0.9999    | 0                   | 0.000046            |
| LogR          | 0.9361    | 0.0510              | 0.065907            |


Model Analysis
The K-Nearest Neighbors (KNN) model excels with very high precision, a low false negative rate, and an extremely low false positive rate, making it highly effective in detecting fraudulent transactions with minimal errors.
The Random Forest (RndFor) model is nearly flawless, boasting almost perfect precision and zero false negatives. It accurately identifies all fraudulent transactions and has an exceptionally low false positive rate, making it an ideal model for this dataset.
In comparison, the Logistic Regression (LogR) model has lower precision and higher false negative and false positive rates. Although it performs reasonably well, it is not as effective as KNN or Random Forest in detecting fraud with minimal errors.

Implications for Detecting Credit Card Fraud
High Precision and Low False Positive Rate

Random Forest (RndFor): This model's nearly perfect precision and negligible false positive rate make it highly reliable for identifying fraudulent transactions with minimal false alarms. This reliability is crucial for maintaining customer trust and satisfaction, as legitimate transactions are less likely to be wrongly flagged.

KNN: With high precision and low error rates, KNN is also a strong alternative to Random Forest.

Low False Negative Rate

Random Forest (RndFor) and KNN: Both models have extremely low false negative rates, with Random Forest achieving zero false negatives. This ensures that fraudulent transactions are rarely missed, significantly reducing potential financial losses due to fraud.

Business Case for Financial Institutions

Reduction in Financial Losses
Effective Fraud Detection: Utilizing highly accurate models like Random Forest or KNN can drastically reduce financial losses from undetected fraudulent transactions. The near-zero false negative rate of these models means that almost all fraudulent activities are identified and stopped in time.

Improved Customer Trust and Satisfaction

Minimizing False Positives: Accurate identification of fraudulent transactions and minimal false positives lead to fewer disruptions for customers. This enhances their trust in the financial institution, as their legitimate transactions are less likely to be flagged incorrectly.

Customer Retention: Satisfied customers are more likely to stay with the institution, leading to higher retention rates.

Operational Efficiency
Resource Allocation: Reliable models allow the institution to allocate fewer resources to manually reviewing transactions, enabling staff to focus on other critical tasks. This improves the efficiency of human resource use and reduces operational costs.

Automated Systems: The reliability of these models supports the development of automated fraud detection systems that can operate in real-time and handle large volumes of transactions without human intervention.

Competitive Advantage

Reputation: A financial institution known for robust fraud detection capabilities gains a competitive edge. Customers are more likely to choose a bank that effectively protects their accounts from fraud.

Market Positioning: Leveraging advanced machine learning models positions the institution as a leader in fintech innovation and security, attracting new customers and partners.

Regulatory Compliance

Meeting Standards: High-performing fraud detection systems help ensure compliance with regulatory standards and guidelines, avoiding potential fines and legal issues.

Reporting and Audits: Accurate and efficient fraud detection facilitates easier reporting and auditing processes, ensuring transparency and accountability.

Conclusion

Adopting highly accurate models like Random Forest and KNN for fraud detection offers substantial benefits for financial institutions. These models minimize financial losses, improve customer satisfaction, enhance operational efficiency, provide a competitive edge, and ensure regulatory compliance. The strong business case for these advanced machine learning models is clear, given their significant positive impact on both the institution's bottom line and customer relations.

## Videos of Learning and Experience


* Sarita Rana: https://drive.google.com/file/d/1J7-f0emnaJabHOkSX0Zo0YLDomFkHgPA/view?usp=drive_link
* Elizabeth Yeo: https://drive.google.com/file/d/16CQnj9jih-SSa84uT4QGoKti-7Boy8Pe/view?usp=drive_link
* Okky Rijanto:
* Gordon Geringas: https://youtu.be/4JVhbL7WqM4


