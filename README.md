# PREDICTING CREDIT CARD FRAUD AGAIN
## Authors: Okky Rijanto, Sarita Rana, Elizabeth Yeo, Gibran Alvarez Aguilar, Gordon Geringas

### Summary
1. Data exploration


- There are no "Null" values in the dataset
- The transaction amount is small. The mean of all the transaction amounts is approx. $88.
- The dataset is highly imbalanced; 99.83% of the transactions were Non-Fraud while 0.17% of the transactions were fraud.
  
![Class Distribution](src/class_dist.png) 

- The features other than "Amount" and "Time" have gone through a PCA transformation and were anonymized.


- Distributions:
  Visualizing the distributions of the "Transaction Time" and "Transaction Amount":


![Transaction Distribution](src/transaction_time_dist.png) 

  Visualizing the distributions of all the features to check their skewness:
  
![All Distribution](src/all_dist.png) 
  
2. Data pre-processing

- Created box plots to visualize the outliers
  
![outliers](src/outliers.png) 

- Removed outliers and duplicates
- Feature scaling: Since the other features have been scaled, we scaled the "Time" and "Amount" using StandardScaler.

### Machine Learning Architecture and Problem Domain motivation
   
Since the data is highly imbalanced, simpler models showed that, despite high accuracy, they did not perform well in fraud detection. Therefore, we explored multiple balancing techniques to improve the model's performance in detecting fraudulent transactions.

Pipelines Implemented:

Pipeline 1: Included SMOTE for data augmentation.

Pipeline 2: Used BalancedRandomForestClassifier, which incorporates an internal balancing mechanism.

Pipeline 3: Applied ADASYN for data augmentation.

Pipeline 4: Baseline model with stratified splitting of the dataset (ensuring the class distribution is maintained in both training and test sets).

Results:

Let's breakdown the Cross-validation results for the three pipelines (pipe1, pipe3, and pipe4) based on the accuracy, f1, and recall metrics.

Pipeline 1 (SMOTE):

Demonstrated a balanced performance with a focus on recall, which is crucial for detecting fraud cases.

1. Accuracy
   
Accuracy measures the proportion of correctly classified instances out of the total instances.

pipe1: array([0.99945138, 0.99947333, 0.99940749, 0.99949527, 0.99951722])

pipe3: array([0.99947333, 0.99945138, 0.99938555, 0.99956111, 0.99947333])

pipe4: array([0.99951722, 0.99945138, 0.99947333, 0.99956111, 0.99958305])

All three pipelines demonstrate very high accuracy, close to 1.0, indicating that almost all instances were classified correctly. The differences in accuracy across the pipelines are minimal, suggesting that each pipeline is highly effective in terms of correctly classifying instances overall.

2. F1 Score
   
The F1 score is the harmonic mean of precision and recall, giving a balanced measure of a model's performance on both the positive and negative classes.

pipe1: array([0.8427673, 0.83333333, 0.82352941, 0.84768212, 0.85714286])

pipe3: array([0.84810127, 0.82758621, 0.81578947, 0.86486486, 0.84615385])

pipe4: array([0.84722222, 0.81481481, 0.82857143, 0.86111111, 0.8707483])

The F1 scores vary more across the pipelines, reflecting how each handles the trade-off between precision and recall. pipe1 and pipe3 show relatively consistent F1 scores, while pipe4 shows a slight improvement, particularly in the higher end of the score range (up to 0.87). This suggests that pipe4 might be slightly better balanced in handling both true positives and minimizing false positives.

3. Recall

Recall (also known as sensitivity) measures the proportion of actual positives correctly identified by the model.

pipe1: array([0.85897436, 0.75949367, 0.79746835, 0.81012658, 0.83544304])

pipe3: array([0.85897436, 0.75949367, 0.78481013, 0.81012658, 0.83544304])

pipe4: array([0.78205128, 0.69620253, 0.73417722, 0.78481013, 0.81012658])

Recall scores show the greatest variation across the pipelines. pipe1 and pipe3 have similar recall scores, with pipe1 slightly better overall. However, pipe4 has lower recall scores, indicating it misses more actual positive cases compared to the other pipelines. This could mean that pipe4 is more conservative in its predictions, leading to fewer false positives but at the cost of more false negatives.

f1_score: 0.8842105263157894

![Confusion matrix](reports/cm_pipe1.png) 

Pipeline 2 (BalancedRandomForestClassifier):
Had the lowest accuracy among the pipelines, suggesting that its internal balancing mechanism may have affected its overall classification ability.

Pipeline 3 (ADASYN):
Showed similar trends to SMOTE but with a different synthetic data generation approach.

f1_score: 0.8645833333333334

![Confusion matrix](reports/cm_pipe2.png) 

Pipeline 4 (Stratified Split):
The stratified split helped maintain the class distribution during model training and testing, leading to the highest F1 score of 0.968. This indicates that careful data splitting without additional balancing techniques can be highly effective, especially when the model naturally handles class imbalance well.

f1_score: 0.968421052631579

![Confusion matrix](reports/cm_pipe4.png) 

Confusion matrices were plotted for each pipeline, highlighting the performance in terms of true positives, true negatives, false positives, and false negatives.
The confusion matrix for Pipeline 4 showed strong performance, with well-balanced precision and recall, further supported by the stratified data split.

Conclusion:
Data balancing techniques like SMOTE and ADASYN generally improve the ability to detect fraud cases by enhancing recall. However, in this case, the baseline model with stratified data splitting outperformed others in terms of F1 score. This suggests that maintaining the natural distribution of classes during training can be more effective than applying synthetic data balancing, especially when using a model that handles class imbalance well.
Based on the results, it is recommended to proceed with Pipeline 4 for production, as it offers the best trade-off between accuracy, precision, and recall, ensuring that fraudulent transactions are detected efficiently without overwhelming the system with false positives.

7. XG Boost (Okky)
8. Data Augmentation using schmiddy (Gibran)
9. Logistic (Gibran)
10. AutoEncoders (Gibran)
11. GAN (Liz)


### Tuning Hyperparameters
To be completed

12. Conclusion
Which is the best model for highly imbalanced dataset? using SMOTE to scale the data prior to loading to XG Boost.
For imbalanced dataset, accuracy is not a good metric so we looked at the F1 score.
Logistic model has the highest F1 Score 0.81

### Limitations:
XG Boost: computational power limitation across most of the methods
GAN: generator and discriminator

### Criteria
We seek to train a model that minimizes [true fraud:predicted notfraud] and maximizes [truefraud : predicted fraud]. Undetected true fraud is strictly damaging to the financial health of the credit institution and clients. Predicting true fraud allows the institution to mitigate harms of fraud by locking the card out of any further transactions. To that extent, we seek a model that can perform better than 1:3 [true fraud:predicted notfraud] : [truefraud : predicted fraud].


### Training / Validation Strategy
To be completed

### Data Ethics Discussion
To be completed

### Individual Reflection Videos
* Okky Rijanto
* Sarita Rana
* Elizabeth Yeo
* Gibran Alvarez Aguilar
* Gordon Geringas

### Repo File and Folder Structures
* **Data:** Contains the raw, processed and final data. For any data living in a database, make sure to export the tables out into the `sql` folder, so it can be used by anyone else.
* **Experiments:** A folder for experiments
* **Models:** A folder containing trained models or model predictions
* **Reports:** Generated HTML, PDF etc. of your report
* **src:** Project source code
* README: This file!
* .gitignore: Files to exclude from this folder, specified by the Technical Facilitator

### Change log
2024-08-07 [Gordon] Added team-project-2 branch and set up README.md
