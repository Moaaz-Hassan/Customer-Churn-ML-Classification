# Customer Churn Classification

This project tackles a binary classification problem to predict whether a customer will **churn** (leave the service) or not, based on their demographic and behavioral data.  

---
## Project Workflow

### 1. Data Understanding 
* Understand Columns
* check dtype
* Describe Numerical Cols
* Describe Categorical Cols
* Catching any error

### 2. Feature Engineering
- Created new features based on business logic and customer behavior.

### 3. Exploratory Data Analysis (EDA)
- Conducted Univariate and Bivariate analysis.
- Visualized relationships between features and churn.

### 4. Preprocessing
* Detect & Handle Duplicates
* train_test_split
* Detect & Handle NaNs
* Detect & Handle Outliers
* Encoding: (Ordinal:[OrdinalEncoder, LabelEncoder] - Nominal: [< 7 uniques(OneHotEncoding), > 7 uniques (BinaryEncoder)])
* Imbalanced: X_train_resampled
* Scaling: StandardScaler, MinMaxScaler, RobustScaler: X_train_resampled_scaled
---

## 5. Modeling & Evaluation

Trained and evaluated several classification models using both SMOTE and RandomUnderSampler:
| Model              | Sampling           | Train Acc | Valid Acc | F1 Score |
|-------------------|--------------------|-----------|-----------|----------|
| LogisticRegression| SMOTE / Under      | 71 / 70   | 70 / 70   | 49 / 49  |
| KNN               | SMOTE / Under      | 59 / 57   | 73 / 73   | 52 / 53  |
| DecisionTree      | SMOTE / Under      | 56 / 57   | 74 / 74   | 53 / 53  |
| SVC               | SMOTE / Under      | 83 / 78   | 74 / 74   | 54 / 54  |
| RandomForest      | SMOTE / Under      | 85 / 82   | 75 / 75   | 54 / 55  |
| XGBoost           | SMOTE / Under      | 83 / 72   | 78 / 78   | 56 / 56  |
| CatBoost          | SMOTE / Under      | 86 / 87   | 79 / 79   | 57 / 57  |

✅ **SMOTE** showed better performance overall, so it was used for final modeling.

## Ensemble Learning

Used the top 3 models (CatBoost, XGBoost, RandomForest) in ensemble techniques:

| Technique | Train Acc | Valid Acc | F1 Score |
|-----------|-----------|-----------|----------|
| Voting    | 86        | 81        | 59       |
| Stacking  | 88        | 81        | 60 ✅     |

- Final model: **Stacking Ensemble**
- ## Final Model Performance on Test Set

After selecting the best ensemble model (**Stacking** using CatBoost, XGBoost, and RandomForest with SMOTE), the final evaluation was done on the **test set**, and the results were:

- **Test Accuracy**: `77.7%`
- **Test F1 Score**: `57.6%`
- **Test Precision**: `46.97%`
- **Test Recall**: `74.45%`


The main goal was to **increase Recall** so the model can correctly find most of the customers who are likely to leave.  
After looking at the **Precision-Recall Curve**, I changed the model’s **threshold** to give more focus on catching those customers — even if that means it might make more mistakes in predicting who will stay.  
This helps companies take early actions to keep their customers before they leave
