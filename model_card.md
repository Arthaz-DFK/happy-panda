## Model Description
**Model Purpose**

This model predicts whether a bank customer will subscribe to a term deposit (i.e., “yes” vs. “no”) after a telemarketing campaign. The goal is to identify high-potential contacts, optimise outreach timing, and tailor marketing strategies.

**Input**

1. Tabular Features from the Bank Marketing dataset (UCI Bank Data), including:
    - Demographics (e.g., age, job, marital status, education).
    - Financial (e.g., balance, loan/housing status).
    - Campaign-specific (e.g., month, day, duration of last call, number of contacts, outcome of previous campaign, etc.).

2. Each row represents a single customer’s data.

**Output**

1. Binary classification:
    - 1 (yes) – the model predicts the customer will subscribe to the term deposit.
    - 0 (no) – the model predicts the customer will not subscribe.

**Model Architecture**

1. XGBoost Classifier
    - Hyperparameters are tuned using Bayesian Optimization (BayesSearchCV from scikit-optimize):
      - Search spaces included learning_rate, max_depth, n_estimators, subsample, etc.
      - Cross-validation strategy: Stratified K-Fold (3 splits).

2. Preprocessing:
    - Label encoding for categorical features (job, marital, etc.).
    - Dropping or encoding “unknown” values.
    - Train/test split (80/20).

3. Pipeline:
    1) Data Loading & Cleaning
    2) Train/Test Split
    3) Bayesian Hyperparameter Optimization
    4) Best XGBoost Model used to predict subscription outcome.

## Performance
**Evaluation Metrics**
    - Accuracy – Overall proportion of correct predictions (yes/no).
    - Precision, Recall, F1 – Focus on the “yes” class, which is smaller (imbalanced).
    - ROC AUC – Measures how well the model ranks positives above negatives across all thresholds.
    - Precision-Recall Curve – Especially useful for imbalanced classification to see how recall changes as we adjust thresholds.

**Summary Results**
    - Accuracy: ~85% on the held-out test set.
    - ROC AUC: ~0.91–0.92, indicating strong separability of classes.
    - Precision (class=1): ~0.69, Recall (class=1): ~0.63, showing moderate ability to identify positive responders.

The model was trained on 80% of the dataset and evaluated on the remaining 20%. Hyperparameters were tuned via 3-fold cross-validation during the Bayesian search to avoid overfitting and to optimize generalization.

## Limitations
1. Imbalanced Classes
    - The dataset typically has more “no” (non-subscribers) than “yes.” Consequently, recall or F1 for the “yes” class may be moderate (~63%).
    - Potentially missing some true positives if the threshold is fixed at 0.5.

2. Time & Seasonal Effects
    - Although features like month and day_of_week are included, external economic or seasonal factors might not be fully captured.

3. Feature Engineering
    - The model relies mostly on standard transformations (label encoding, dropping “unknown”). More advanced engineering (e.g., domain-specific transformations, external macroeconomic data) could improve performance but wasn’t included here.

4. Interpretability
    - XGBoost is a tree-ensemble method. While SHAP and partial dependence help interpret results, it’s not as straightforward as linear models with explicit coefficients.

## Trade-offs
1. Precision vs. Recall
    - If the business goal is to minimise missed opportunities (i.e., want more “yes”), lowering the decision threshold will boost recall but increase false positives (more “no” predicted as “yes”).
    - If the goal is to conserve campaign resources, a higher threshold yields fewer contacts (higher precision) but risks missing potential subscribers.

2. Complexity vs. Runtime
    - Bayesian optimization adds computational overhead compared to a default XGBoost. However, it typically yields better hyperparameters and model performance.

3. Interpretability vs. Accuracy
    - Tree ensembles can produce higher accuracy than simpler methods (like logistic regression), but are less transparent. We mitigated this by using SHAP for local/global feature impact and partial dependence plots.

4. Data Granularity
    - Dropping “unknown” values may simplify modeling but can reduce the dataset size. Keeping them with a separate “unknown” category might add noise or reveal patterns in how “unknown” correlates with subscription.

## Final Note
This model provides actionable insights to prioritize contacting likely subscribers, refine when to contact (based on partial dependence for month/day), and identify how to personalise campaigns (via top features like “duration” or “poutcome”). Users should consider the above limitations and trade-offs when deploying or extending this solution.

