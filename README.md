# PROJECT TITLE 
PORTFOLIO PROJECT ON OPTIMIZING A MODEL FOR REAL-LIFE DATA

## NON-TECHNICAL EXPLANATION OF YOUR PROJECT
This project aims to help a bank identify which customers are most likely to respond positively to a marketing campaign for term deposits. By using data about each customer’s demographics, financial history, and past interactions, I train a machine learning model that highlights the best people to contact. I also analyse the ideal timing to reach out and how to personalise communication. Ultimately, this saves time and resources by focusing on high-potential customers. It’s like giving the bank a roadmap, so they know who to contact, when to contact them, and what message will best resonate with each customer.

## DATA
For this project, we use the UCI Bank Marketing Dataset, a publicly available set of records from a Portuguese bank’s marketing campaigns. It includes demographic attributes (like age, job, marital status), financial variables (balance, loan), and campaign details (contact type, day, month, outcomes of previous campaigns). All data is numeric or categorical; unknown values have been dropped or encoded. The original dataset can be found at the UCI Machine Learning Repository. We cite this repository as our primary data source. 
Location: archive.ics.uci.edu/dataset/222/bank+marketing

## MODEL 
I employ an XGBoost classification model. I chose this model because:

- It handles tabular data effectively, even with heterogeneous (categorical + numeric) features.
- It often outperforms simpler methods on structured data.
- It provides feature importances and integrates well with interpretability tools like SHAP for deeper insights.

Additionally, XGBoost is robust to overfitting and handles class imbalance moderately well (important for a marketing scenario where the positive “yes” class is smaller).

## HYPERPARAMETER OPTIMSATION
I tune hyperparameters such as:

- learning_rate, max_depth, n_estimators, gamma, subsample, colsample_bytree, reg_alpha, and reg_lambda.

To optimize them, I use Bayesian Optimisation via BayesSearchCV. This method balances exploration and exploitation to find better hyperparameters in fewer iterations than a random or grid search. A 3-fold Stratified Cross-Validation is performed during the optimisation to ensure we don’t overfit to a single split.

## RESULTS
After training, we evaluate on a 20% test split. Key results:

- Accuracy: ~85%
- ROC AUC: ~0.91, indicating the model distinguishes well between customers who do and don’t subscribe.
- The model’s precision and recall for the “yes” class are moderate (~0.69 precision, ~0.63 recall), which is acceptable given the imbalanced data.

I also produced partial dependence plots to see how timing features (month/day) affect outcomes, and used SHAP to understand how each variable (like call duration, previous campaign outcome, housing loan) influences individual predictions.

I conclude that the model provides a useful way to target high-likelihood customers, adjust outreach timing, and tailor messages based on top drivers such as previous campaign outcome, call duration, and loan status.

