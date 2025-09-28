# bankingproject

This project is a machine learning project for the banking industry.

## CRISP-DM Methodology

This project follows the Cross-Industry Standard Process for Data Mining (CRISP-DM) methodology to ensure a structured and effective approach.

### 1. Business Understanding
- **Objective**: To build a predictive model that identifies clients with the highest likelihood of subscribing to a term deposit.
- **Goal**: Enhance marketing campaign efficiency by focusing resources on high-probability leads, thereby increasing conversion rates and reducing costs.

### 2. Data Understanding
- **Source**: The data is from a Portuguese banking institution, collected from direct marketing campaigns.
- **Exploration**: Initial analysis (EDA) was performed to understand the distribution of variables, identify imbalances in the target variable, and discover initial correlations between features and client subscriptions. Key insights revealed that factors like previous campaign success, contact method (cellular), and certain economic indicators were strong predictors.

### 3. Data Preparation
- **Cleaning**: The `y` column was renamed to `target` and converted to a binary format (1/0).
- **Feature Engineering**: 
    - The `pdays` column was transformed into a binary feature indicating previous contact.
    - The `duration` column was dropped as it is not a realistic predictor (post-call information).
- **Encoding**: All categorical features (e.g., `job`, `marital`, `education`) were one-hot encoded to be used in the models.

### 4. Modeling
- **Initial Models**: Four classifiers were trained and compared: Logistic Regression, K-Nearest Neighbors, Decision Tree, and SVM.
- **Feature Expansion**: Models were re-evaluated using the full feature set, which significantly improved performance over a limited, basic feature set.
- **Hyperparameter Tuning**: GridSearchCV was used to tune the Decision Tree model, which improved its accuracy and addressed overfitting.
- **Addressing Class Imbalance**:
    - **Feature Selection**: A model was trained on a smaller, curated set of features, which did not improve performance.
    - **Class Weighting**: The `class_weight='balanced'` parameter was applied to Logistic Regression, Decision Tree, and SVM models. This proved to be the most effective strategy.

### 5. Evaluation
- **Initial Metric**: Overall accuracy was used as a baseline metric. However, due to severe class imbalance, it was found to be misleading.
- **Advanced Metrics**: The focus shifted to the **Classification Report** and **Confusion Matrix**, with a specific emphasis on **Recall** for the 'Yes' class.
- **Key Finding**: The `class_weight='balanced'` strategy dramatically improved recall for the subscriber class from ~46% to **73%** (with the SVM model), successfully achieving the business goal of capturing more potential customers, despite a slight drop in overall accuracy.

### 6. Deployment
- **Recommendation**: The **SVM model with `class_weight='balanced'`** is recommended for deployment. It offers the highest recall, making it the most effective tool for generating a comprehensive list of marketing leads.
- **Alternative**: If model interpretability is a business requirement, the **Decision Tree model with `class_weight='balanced'`** is a strong second choice, offering comparable performance.
