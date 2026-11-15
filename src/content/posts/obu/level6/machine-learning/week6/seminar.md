---
title: "Week 6 Seminar - GridSearchCV and Learning Curve"
published: 2026-11-12
publishedAt: 2026-11-12T17:15:00+08:00
description: "This week only contains some tips."
image: "./152096547.png"
tags: ["Python", "Jupyter", "Dataset", "GridSearchCV", "Decision Tree", "Learning Curve"]
category: "Machine Learning"
draft: false
pinned: false
lang: zh_CN
---

运行老师提供的 `ipynb` 前需要做以下修改：

- 按实际情况修改第二个单元格中的数据集路径。

```python
# Load the csv data

df = pd.read_csv('chronic_kidney_disease.csv')
```

- 在“Logistic Regression with GridSearchCV”一节对应的代码开头增加这些库导入（已有的 `from sklearn.model_selection import GridSearchCV` 不要删）。

```python
from imblearn.pipeline import make_pipeline
from imblearn.over_sampling import SVMSMOTE
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
```

- “AdaBoost with GridSearchCV”一节的 `AdaBoostClassifier` 中，新版本的库不支持 `algorithm='SAMME'` ，需要去掉才能运行。

```python
from sklearn.ensemble import AdaBoostClassifier
# Define the AdaBoost model
# We use SAMME in AdaBoost because the older SAMME.R algorithm is deprecated in our scikit-learn version. 
# SAMME combines several weak classifiers to build a stronger model and avoids the deprecation warnings
ada_tuned = make_pipeline(
    preprocessor,
    SVMSMOTE(random_state=42),
    AdaBoostClassifier(
        # algorithm='SAMME',
        random_state=42
    )
)
```

- “Voting Classifier with GridSearchCV”一节对应的代码存在警告。

```
FutureWarning: The `probability` parameter was deprecated in 1.9 and will be removed in version 1.11. Use `CalibratedClassifierCV(SVC(), ensemble=False)` instead of `SVC(probability=True)`
  warnings.warn(
```

需要增加导入 `from sklearn.calibration import CalibratedClassifierCV` 并使用 `CalibratedClassifierCV(SVC(), ensemble=False)` 来代替 `SVC(probability=True)` ；另外还需要把 `votingclassifier__svm__C` 改为 `votingclassifier__svm__estimator__C`  
修改后的代码类似于：

```python
from sklearn.ensemble import VotingClassifier
from sklearn.calibration import CalibratedClassifierCV

# Define the base classifiers
base_models = [
    ('lr', LogisticRegression(max_iter=1000)),
    # ('svm', SVC(probability=True)),
    ('svm', CalibratedClassifierCV(SVC(), ensemble=False)),
    ('dt', DecisionTreeClassifier(random_state=42))
]

# Define the Voting Classifier
voting_tuned = make_pipeline(
    preprocessor,
    SVMSMOTE(random_state=42),
    VotingClassifier(
        estimators=base_models,
        voting='soft'
    )
)

# Define the hyperparameter grid
param_grid = {
    'votingclassifier__lr__C': [0.1, 1, 10],
    # 'votingclassifier__svm__C': [0.1, 1, 10]
    'votingclassifier__svm__estimator__C': [0.1, 1, 10]
}
```

- “Compare all 15 classifiers”一节对应的代码缺少 `models` 字典，需要添加。

```python
from sklearn.metrics import (
    accuracy_score, precision_score, recall_score,
    f1_score, confusion_matrix, roc_auc_score
)
import pandas as pd

results = []

# Store all 15 trained GridSearchCV models

models = {
    'Logistic Regression': search_lr,
    'SVM': search_svm,
    'Decision Tree': search_dt,
    'Random Forest': search_rf,
    'AdaBoost': search_ada,
    'Gradient Boosting': search_gb,
    'KNN': search_knn,
    'Stacking': search_stack,
    'Voting': search_voting,
    'LightGBM': search_lgbm,
    'CatBoost': search_cat,
    'XGBoost': search_xgb,
    'Bagging': search_bag,
    'Extra Trees': search_et,
    'Gaussian NB': search_gnb
}
```

- “Learning curves for all 15 classifiers”一节对应的代码存在警告。

```
FutureWarning: The `probability` parameter was deprecated in 1.9 and will be removed in version 1.11. Use `CalibratedClassifierCV(SVC(), ensemble=False)` instead of `SVC(probability=True)`
  warnings.warn(
```

该警告随“Voting Classifier with GridSearchCV”一节修复。

附修改完毕的 Interactive Python Notebook 文件：<a href="/obu/level6/machine-learning/week6/GridSearchCV_and_Learning_Curve-fixed.ipynb" download>GridSearchCV_and_Learning_Curve-fixed.ipynb</a>

::: tip[温馨提示]
本周的代码执行时间较长，需要耐心等待。以我的 Intel E5 2698 v4 (分配了8个核心) 为例，执行完全部32个单元格耗时692秒，最后几个单元格耗时尤其长。
:::

Source: [gridsearchcv-and-learning-curveipynb.zip](https://vle.zycdut.net/sites/student.zy.cdut.edu.cn/files/attachments/gridsearchcv-and-learning-curveipynb.zip)
