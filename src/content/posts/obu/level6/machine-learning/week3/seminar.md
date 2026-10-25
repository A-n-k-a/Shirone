---
title: "Seminar: Data Splitting, Data Scaling, Data Imbalance, Logistic Regression, KNN, Confusion Matrix, and evaluation metrics"
published: 2026-10-22
publishedAt: 2026-10-22T17:15:00+08:00
description: "This week only contains code and some tips."
image: "./150972939.jpg"
tags: ["Python", "Jupyter", "Dataset"]
category: "Machine Learning"
draft: false
pinned: false
lang: zh_CN
---

本周的练习需要额外安装 `imblearn` 库，如果是根据我的非 conda 安装方式，只需要在激活虚拟环境后用 `pip` 安装即可。  

```bash
source ml_chc6089/bin/activate
pip install imblearn
```

如果安装了 Anaconda，请在 Anaconda 中安装。

---

老师提供的代码的 Data split 单元格（`In[48]`）虽然将分类标签替换为了 `0` 和 `1`，但在某些 pandas 版本中，替换后可能仍保留 `object` 数据类型。

`SVMSMOTE` 内部调用 scikit-learn 检查目标标签，此时就可能得到：

```
ValueError: Unknown label type: unknown
```

推荐的修复：

找到 Data split 标题下的代码，将标签转换语句修改为：

```python
# Convert classification labels to 0 and 1
y = y.replace({
    'ckd': 1,
    'not ckd': 0,
    'notckd': 0
}).astype('int64')
```

之后的 SVMSMOTE 代码可以保持不变，也可以在执行 SVMSMOTE 前检查：

```python
from sklearn.utils.multiclass import type_of_target

print(y_train.dtype)
print(type_of_target(y_train))
print(y_train.value_counts())
```

修复后，正常情况下应该得到：
- 数据类型：`int64`
- 标签类型：`binary`
- 标签分布：`1` 有 200 个样本，`0` 有 120 个样本

---

额外的潜在问题：

数据预处理中的 `inplace=True` 用法

在前面的 `replace incorrect values` 单元格中：

```python
df['dm'] = df['dm'].replace(
    to_replace={'\tno':'no','\tyes':'yes',' yes':'yes'},
    inplace=True
)
```

存在错误写法，应该移除 `inplace=True`：

```python
df['dm'] = df['dm'].replace(
    to_replace={'\tno':'no','\tyes':'yes',' yes':'yes'}
)
```

---

已修正的 Interactive Python Notebook ：<a href="/obu/level6/machine-learning/week3/machine-learning_week3_seminar-fixed.ipynb" download>machine-learning_week3_seminar-fixed.ipynb</a>

Source: [week-3-seminaripynb.zip](https://vle.zycdut.net/sites/student.zy.cdut.edu.cn/files/attachments/week-3-seminaripynb.zip)
