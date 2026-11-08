---
title: "Week 5 Seminar - Classification Algorithms 2 & Ensemble Learning"
published: 2026-11-05
publishedAt: 2026-11-05T17:15:00+08:00
description: "This week only contains some tips."
image: "./139835174.png"
tags: ["Python", "Jupyter", "Dataset", "Support Vector Machine", "Decision Tree", "Random Forest", "AdaBoost", "Stacking", "Voting", "LightGBM", "CatBoost", "XGBoost", "Bagging", "ROC-AUC"]
category: "Machine Learning"
draft: false
pinned: false
lang: en
---

In soft voting section, you may encounter warning (or even error in the future):

```
/opt/CHC6089/ml_chc6089/lib/python3.14/site-packages/sklearn/svm/_base.py:236: FutureWarning: The `probability` parameter was deprecated in 1.9 and will be removed in version 1.11. Use `CalibratedClassifierCV(SVC(), ensemble=False)` instead of `SVC(probability=True)`
  warnings.warn(
```

Solution:

Add this import at beginning:

```python
from sklearn.calibration import CalibratedClassifierCV
```

Use `CalibratedClassifierCV(SVC(), ensemble=False)` instead of `SVC(probability=True)`.

---

The code in this cell should look like this:

```python
#soft voting
from sklearn.ensemble import VotingClassifier
from sklearn.calibration import CalibratedClassifierCV

voting = VotingClassifier(
    estimators=[
        ("dt", DecisionTreeClassifier()),
        ("rf", RandomForestClassifier()),
        ("svm", CalibratedClassifierCV(SVC(), ensemble=False))
    ],
    voting="soft"
)

voting.fit(x_train, y_train)

y_pred_voting = voting.predict(x_test)
```

Source: [week5-seminar.zip](https://vle.zycdut.net/sites/student.zy.cdut.edu.cn/files/attachments/week5-seminar.zip)
