---
title: "Week 4 Seminar - Feature Selection"
published: 2026-10-29
publishedAt: 2026-10-29T17:15:00+08:00
description: "Feature Selection using LASSO, RFE and Boruta Techniques."
image: "./64846291.jpg"
tags: ["Python", "Jupyter", "Dataset", "LASSO", "RFE", "Boruta"]
category: "Machine Learning"
draft: false
pinned: false
lang: en
---

```python
#Remember, the following files already contain:
#x_train: Scaled and balanced training features.
#y_train: Balanced training labels.
#x_test: Scaled testing features, without SMOTE.
#y_test: Original testing labels.
#We do not need to apply StandardScaler or SVMSMOTE again.



import pandas as pd

# Load the processed datasets
train_data = pd.read_csv("CKD_Training_Processed.csv")
test_data = pd.read_csv("CKD_Testing_Processed.csv")

# Separate features and target
x_train = train_data.drop(columns=['classification'])
y_train = train_data['classification']

x_test = test_data.drop(columns=['classification'])
y_test = test_data['classification']

print("Training dataset:", train_data.shape)
print("Testing dataset:", test_data.shape)
print("Training dataset:", x_train.shape)
print("Testing dataset:", x_test.shape)
```

## Applying LASSO

### LassoCV

```python
from sklearn.linear_model import LassoCV
from sklearn.feature_selection import SelectFromModel
import matplotlib.pyplot as plt
import numpy as np

# Get the feature names from the training dataset
feature_names = x_train.columns

# Initialize LASSO with 5-fold cross-validation
lasso = LassoCV(cv=5, random_state=42)

# Fit LASSO using the training dataset
lasso.fit(x_train, y_train)

# Select important features using LASSO
model = SelectFromModel(lasso, prefit=True)

# Apply feature selection to training and testing datasets
# .values avoids the feature names warning
x_train_lasso = model.transform(x_train.values)
x_test_lasso = model.transform(x_test.values)

# Display the number of selected features
print(f"LASSO selected {x_train_lasso.shape[1]} features out of {x_train.shape[1]}")

# Get the names of selected features
selected_features_lasso = feature_names[model.get_support()]

print("\nSelected Features from LASSO:")
print(selected_features_lasso.tolist())

# Display the best alpha value
print("\nBest alpha:", lasso.alpha_)

# Plot the coefficients of all features
plt.figure(figsize=(10, 6))
plt.barh(feature_names, lasso.coef_, color='skyblue')
plt.xlabel('Coefficient Value')
plt.ylabel('Features')
plt.title('Feature Importance by LASSO Coefficients')
plt.gca().invert_yaxis()
plt.tight_layout()
plt.show()
```

### Lasso (Manual)

```python
from sklearn.linear_model import Lasso
from sklearn.feature_selection import SelectFromModel
import matplotlib.pyplot as plt

# Get the feature names from the training dataset
feature_names = x_train.columns

# Initialize LASSO with a fixed alpha value
lasso = Lasso(alpha=0.01, max_iter=10000)

# Fit LASSO using the training dataset
lasso.fit(x_train, y_train)

# Select important features using LASSO
model = SelectFromModel(lasso, prefit=True)

# Apply feature selection to training and testing datasets
x_train_lasso = model.transform(x_train.values)
x_test_lasso = model.transform(x_test.values)

# Display the number of selected features
print(f"LASSO selected {x_train_lasso.shape[1]} features out of {x_train.shape[1]}")

# Get selected feature names
selected_features_lasso = feature_names[model.get_support()]

print("\nSelected Features from LASSO:")
print(selected_features_lasso.tolist())

# Get eliminated feature names
eliminated_features_lasso = feature_names[~model.get_support()]

print("\nEliminated Features from LASSO:")
print(eliminated_features_lasso.tolist())

# Display alpha value
print("\nAlpha:", lasso.alpha)

# Plot LASSO coefficients
plt.figure(figsize=(10, 6))
plt.barh(feature_names, lasso.coef_, color='skyblue')
plt.axvline(x=0, color='red', linestyle='--')
plt.xlabel('Coefficient Value')
plt.ylabel('Features')
plt.title('Feature Importance by LASSO Coefficients (Alpha = 0.01)')
plt.gca().invert_yaxis()
plt.tight_layout()
plt.show()
```

In our first experiment, we used LassoCV, which automatically selected alpha through five-fold cross-validation. It chose approximately 0.00275 and eliminated only one feature.

In our second experiment, we manually increased alpha to 0.01. As a result, LASSO eliminated three features.

This demonstrates that alpha controls the strength of regularisation and influences how many features remain in the model. However, eliminating more features does not necessarily mean achieving better prediction accuracy.

## Feature Selection using RFE Techniques

```python
from sklearn.feature_selection import RFECV
from sklearn.linear_model import LogisticRegression
import matplotlib.pyplot as plt
import numpy as np

# Get the actual feature names from the training dataset
feature_names = x_train.columns

# Use Logistic Regression as the base model for RFE
rfe_model = LogisticRegression(max_iter=1000, random_state=42)

# Initialize RFECV to find the optimal number of features
rfecv = RFECV(estimator=rfe_model, step=1, cv=5,
              scoring='accuracy', n_jobs=-1)

# Fit RFECV using the training dataset
rfecv.fit(x_train, y_train)

# Apply feature selection to training and testing datasets
x_train_rfe = rfecv.transform(x_train)
x_test_rfe = rfecv.transform(x_test)

print(f"RFECV selected {x_train_rfe.shape[1]} features out of {x_train.shape[1]}")

# Get the selected features
selected_features_rfe = [
    feature for feature, support in zip(feature_names, rfecv.support_)
    if support
]

print("\nSelected Features from RFECV:")
print(selected_features_rfe)

# Get the eliminated features
eliminated_features_rfe = [
    feature for feature, support in zip(feature_names, rfecv.support_)
    if not support
]

print("\nEliminated Features from RFECV:")
print(eliminated_features_rfe)

# Display the optimal number of features
print("\nOptimal number of features:", rfecv.n_features_)

# Plot the cross-validation accuracy for different numbers of features
plt.figure(figsize=(10, 6))
plt.plot(
    range(1, len(rfecv.cv_results_['mean_test_score']) + 1),
    rfecv.cv_results_['mean_test_score'],
    marker='o', linestyle='-', color='b'
)
plt.xlabel('Number of features selected')
plt.ylabel('Cross-validation score (accuracy)')
plt.title('Optimal Number of Features Selection with RFECV')
plt.tight_layout()
plt.show()

# Get feature rankings
ranking = rfecv.ranking_

# Green = selected, Red = eliminated
colors = ['green' if rank == 1 else 'red' for rank in ranking]

plt.figure(figsize=(10, 6))
plt.barh(feature_names, ranking, color=colors)

plt.xlabel('Feature Ranking (1 = Selected, Higher = Eliminated Earlier)')
plt.ylabel('Features')
plt.title('Feature Selection Ranking by RFECV')

plt.gca().invert_yaxis()
plt.tight_layout()
plt.show()
```

We use Logistic Regression in RFECV because RFECV needs a machine learning model to determine which features are important and which should be eliminated.

Let's explain using our CKD dataset.

1. Why does RFECV need Logistic Regression? <br>Your CKD dataset has 24 features, such as:
    - age — Age
    - bp — Blood pressure
    - hemo — Hemoglobin
    - sg — Specific gravity
    - al — Albumin

And our target is classification, which has two classes: CKD and Not CKD.

Logistic Regression is suitable because it is a classification algorithm for predicting two classes.

More importantly, Logistic Regression calculates a coefficient for every feature. RFECV uses these coefficients to decide which features to remove.

The first graph illustrates how Recursive Feature Elimination with Cross-Validation identifies the optimal number of features. We started with 24 features and evaluated different feature subsets using Logistic Regression and five-fold cross-validation.

As the number of features increased, classification accuracy generally improved. However, after approximately 15 features, adding more features did not produce a meaningful improvement.

RFECV selected 15 features because this subset achieved the highest cross-validation accuracy while using fewer features than other equally accurate subsets.

This demonstrates an important principle in machine learning: using more features does not always produce a better model.

Unlike feature importance scores, RFECV rankings are ordered so that lower values are better. A ranking of 1 means the feature was selected. A ranking greater than 1 means it was eliminated. The larger the ranking number, the earlier the feature was removed during recursive elimination.
## Feature Selection using Boruta Techniques

```bash
source ml_chc6089/bin/activate
pip install boruta
```

```python
from boruta import BorutaPy
from sklearn.ensemble import RandomForestClassifier
import matplotlib.pyplot as plt
import numpy as np

# Get the actual feature names from the training dataset
feature_names = x_train.columns

# Use Random Forest as the base model for Boruta
boruta_model = RandomForestClassifier(
    n_jobs=-1, max_depth=5, random_state=42
)

# Initialize Boruta
boruta = BorutaPy(
    estimator=boruta_model,
    n_estimators='auto',
    random_state=42
)

# Fit Boruta using the training dataset
boruta.fit(x_train.values, y_train.values)

# Apply feature selection to training and testing datasets
x_train_boruta = boruta.transform(x_train.values)
x_test_boruta = boruta.transform(x_test.values)

# Display the number of selected features
print(f"Boruta selected {x_train_boruta.shape[1]} features out of {x_train.shape[1]}")

# Get selected feature names
selected_features_boruta = [
    feature for feature, support in zip(feature_names, boruta.support_)
    if support
]

print("\nSelected Features from Boruta:")
print(selected_features_boruta)

# Get eliminated feature names
eliminated_features_boruta = [
    feature for feature, support in zip(feature_names, boruta.support_)
    if not support
]

print("\nNot Selected Features from Boruta:")
print(eliminated_features_boruta)

# Get feature rankings
ranking = boruta.ranking_

# Plot the feature rankings
plt.figure(figsize=(10, 6))
plt.barh(feature_names, ranking, color='skyblue')
plt.xlabel('Feature Importance Ranking (Lower is Better)')
plt.ylabel('Features')
plt.title('Feature Importance as Ranked by Boruta')
plt.gca().invert_yaxis()
plt.tight_layout()
plt.show()
```

### Explanation of Random Forest and Boruta Parameters

**1. RandomForestClassifier Parameters**

- **`n_jobs=-1`**: Uses all available CPU cores to perform calculations in parallel, helping to speed up the training process. For example, `n_jobs=1` uses one CPU core, while `n_jobs=-1` uses all available cores.
- **`max_depth=5`**: Limits the maximum depth of each decision tree to 5. This controls tree complexity and can help reduce overfitting.
- **`random_state=42`**: Sets a fixed random seed to make the results reproducible. Using the same random seed helps produce consistent results when running the code multiple times.

**2. BorutaPy Parameters**

- **`estimator=boruta_model`**: Specifies the machine learning algorithm used by Boruta to calculate feature importance. In our experiment, we use Random Forest.
- **`n_estimators='auto'`**: Allows Boruta to automatically determine the number of decision trees used by Random Forest during feature selection.
- **`random_state=42`**: Controls the randomness in Boruta, particularly when creating shuffled copies of the original features (shadow features), ensuring reproducible results.

**3. How Boruta Works**

Boruta creates randomly shuffled copies of the original features, called *shadow features*. It then uses Random Forest to calculate and compare the importance of the original features against these shadow features.

Features that consistently demonstrate significantly greater importance than the shadow features are confirmed as important. Other features may be rejected or remain tentative.

**Key Point:** Random Forest calculates feature importance, while Boruta uses that importance to determine which features should be selected or eliminated.

Boruta is a feature selection algorithm, not a classification model. It needs another machine learning algorithm to calculate feature importance. Random Forest is commonly used because it provides importance scores for each feature. Boruta then compares those scores against shuffled shadow features to decide which features should be retained.

## Compare Feature Selection Methods Using KNN

```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score
import pandas as pd

# Initialize KNN
knn = KNeighborsClassifier(n_neighbors=6)

# 1. KNN using all original features
knn.fit(x_train, y_train)
accuracy_all = accuracy_score(y_test, knn.predict(x_test))

# 2. KNN using LASSO-selected features
knn.fit(x_train_lasso, y_train)
accuracy_lasso = accuracy_score(y_test, knn.predict(x_test_lasso))

# 3. KNN using RFECV-selected features
knn.fit(x_train_rfe, y_train)
accuracy_rfe = accuracy_score(y_test, knn.predict(x_test_rfe))

# 4. KNN using Boruta-selected features
knn.fit(x_train_boruta, y_train)
accuracy_boruta = accuracy_score(y_test, knn.predict(x_test_boruta))

# Compare accuracy results
results = pd.DataFrame({
    'Method': ['All Features', 'LASSO', 'RFECV', 'Boruta'],
    'Number of Features': [
        x_train.shape[1],
        x_train_lasso.shape[1],
        x_train_rfe.shape[1],
        x_train_boruta.shape[1]
    ],
    'Accuracy (%)': [
        accuracy_all * 100,
        accuracy_lasso * 100,
        accuracy_rfe * 100,
        accuracy_boruta * 100
    ]
})

print(results.round(2).to_string(index=False))
```

Source: [week4seminarfeatureselection.zip](https://vle.zycdut.net/sites/student.zy.cdut.edu.cn/files/attachments/week4seminarfeatureselection.zip)
