---
title: "Week 4 Lecture: Feature selection"
published: 2026-10-27
publishedAt: 2026-10-27T16:25:00+08:00
description: "Feature selection is an important stage of machine learning in which we identify the input variables that contribute useful information to prediction. Instead of using every available feature, we aim to retain a relevant subset that supports accurate and interpretable models."
image: "./92388744.png"
tags: ["Supervised Learning", "Training", "Feature selection", "LASSO", "RFE", "Boruta"]
category: "Machine Learning"
draft: false
pinned: false
lang: en
---

## Feature Selection

> Feature selection is an important stage of machine learning in which we identify the input variables that contribute useful information to prediction. Instead of using every available feature, we aim to retain a relevant subset that supports accurate and interpretable models.

Keep the useful features. Remove the unnecessary ones.

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:12px; align-items:center; white-space:nowrap;">
    <div style="background:#f0f8fa; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">All features</span>
    </div>
    <div style="font-size:40px; color:#00969d;">➔</div>
    <div style="background:#e6f7f9; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Feature selection</span>
    </div>
    <div style="font-size:40px; color:#00969d;">➔</div>
    <div style="background:#f0f8fa; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Useful features</span>
    </div>
  </div>
</div>

The goal is to retain useful variables, not simply the fewest variables.

## Learning outcomes

- Explain what feature selection means and why we use it.
- Recognise filter, wrapper, and embedded methods.
- Describe how LASSO, RFE, and Boruta select features.
- Compare the methods and choose one for a simple problem.

> By the end of this lecture, you should understand the purpose of feature selection and distinguish between filter, wrapper, and embedded approaches. You should also be able to explain the working principles of LASSO, Recursive Feature Elimination (RFE), and Boruta.

## What is a feature

> A feature is an individual measurable property or characteristic used by a machine learning algorithm to make predictions. In chronic kidney disease (CKD) classification, blood pressure and haemoglobin may be input features, while the patient’s CKD status is the target variable.

A feature is a piece of information used to make a prediction.

<span style="color: #008B95"><b>Example: Predict whether a patient has CKD.</b></span>  
<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:12px; align-items:center; white-space:nowrap;">
    <div style="background:#f0f8fa; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Age</span>
    </div>
    <div style="background:#f0f8fa; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Blood pressure</span>
    </div>
    <div style="background:#f0f8fa; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Haemoglobin</span>
    </div>
    <div style="background:#ffeeda; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">CKD / Not CKD</span>
    </div>
  </div>
</div>

A feature is an input that a model uses to make a prediction. The target is the answer we want the model to learn

<span style="color: #5D6E7D">The target is what we want to predict; it is not an input feature.</span>

## What is feature selection

Feature selection means choosing the most useful existing features and leaving out less useful ones.

> Feature selection is the process of identifying a subset of relevant input variables from the original dataset. For example, a patient identifier generally does not describe the patient’s medical condition and should not be treated as a meaningful clinical predictor.

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:12px; align-items:center; white-space:nowrap;">
    <div style="background:#f0f8fa; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Age</span>
    </div>
    <div style="background:#f0f8fa; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Patient ID</span>
    </div>
    <div style="background:#f0f8fa; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Haemoglobin</span>
    </div>
    <div style="background:#f0f8fa; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Blood pressure</span>
    </div>
  </div>
</div>

<span style="color: #5D6E7D">Illustrative choice for CKD prediction:</span>

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:12px; align-items:center; white-space:nowrap;">
    <div style="background:#e0f7f9; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Age</span>
    </div>
    <div style="background:#e0f7f9; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Haemoglobin</span>
    </div>
    <div style="background:#e0f7f9; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000022;">
      <span style="font-size:20px; font-weight:600; color:#222d38;">Blood pressure</span>
    </div>
    <div style="background:#ffffff; border-radius:24px; padding:20px 40px; box-shadow: 0 2px 6px #00000000;">
      <span style="font-size:20px; font-weight:600; color:#556070;">Patient ID is usually not clinically meaningful.</span>
    </div>
  </div>
</div>

A patient ID is a record identifier, not a clinical measurement.

## Why select features

- Reduce noise from irrelevant information.
- Make a model easier to explain.
- Often reduce training time and complexity.
- Sometimes improve performance on unseen data.

> Feature selection can reduce irrelevant information, simplify the model, and lower computational cost. It may also improve generalisation by limiting the influence of noisy variables. However, removing features does not automatically improve accuracy, so the selected subset must be evaluated.

<span style="color: #008B95"><b>Feature selection may also reduce overfitting, but accuracy is not guaranteed to improve. Students should always compare performance before and after selecting features.</b></span>

## Three families of feature selection

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:24px; align-items:flex-start; white-space:nowrap;">
    <!-- Filter Column -->
    <div style="display:flex; flex-direction:column; gap:16px;">
      <div style="background:#008b94; border-radius:20px; padding:24px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
        <span style="font-size:24px; font-weight:700; color:#ffffff;">FILTER</span>
      </div>
      <div style="background:#f0f7fa; border-radius:20px; padding:24px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
        <span style="font-size:20px; font-weight:600; color:#222d38;">Use statistical scores</span>
      </div>
      <div style="padding:12px 0; text-align:center;">
        <span style="font-size:20px; font-weight:600; color:#222d38;">Example: correlation</span>
      </div>
    </div>
    <!-- Wrapper Column -->
    <div style="display:flex; flex-direction:column; gap:16px;">
      <div style="background:#008b94; border-radius:20px; padding:24px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
        <span style="font-size:24px; font-weight:700; color:#ffffff;">WRAPPER</span>
      </div>
      <div style="background:#f0f7fa; border-radius:20px; padding:24px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
        <span style="font-size:20px; font-weight:600; color:#222d38;">Try features with a model</span>
      </div>
      <div style="padding:12px 0; text-align:center;">
        <span style="font-size:20px; font-weight:600; color:#222d38;">Example: RFE , Boruta</span>
      </div>
    </div>
    <!-- Embedded Column -->
    <div style="display:flex; flex-direction:column; gap:16px;">
      <div style="background:#008b94; border-radius:20px; padding:24px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
        <span style="font-size:24px; font-weight:700; color:#ffffff;">EMBEDDED</span>
      </div>
      <div style="background:#f0f7fa; border-radius:20px; padding:24px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
        <span style="font-size:20px; font-weight:600; color:#222d38;">Select while training</span>
      </div>
      <div style="padding:12px 0; text-align:center;">
        <span style="font-size:20px; font-weight:600; color:#222d38;">Example: LASSO</span>
      </div>
    </div>
  </div>
</div>

> Feature selection techniques are commonly grouped into three categories. Filter methods use statistical relationships, wrapper methods evaluate features through repeated model fitting, and embedded methods perform selection as part of model training. Boruta is a model-based, wrapper-style approach.

## Filter methods: quick screening

- Score each feature using a statistical relationship with the target.
- Choose the highest-scoring features.
- Usually fast because they do not repeatedly train a prediction model.

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:12px; align-items:center; white-space:nowrap;">
    <div style="background:#e0f7f9; border-radius:24px; padding:16px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
      <span style="font-size:24px; font-weight:600; color:#222d38;">Example: rank CKD features using mutual information</span>
    </div>
  </div>
</div>

> Filter methods rank or score features using a statistical criterion, such as correlation or mutual information. Features with higher scores are selected without repeatedly training the final predictive model. This makes filter methods relatively fast, although they may overlook interactions between features.

For instance, mutual information can help rank CKD measurements by their association with the target. This screening is usually faster than repeatedly fitting a model.

## LASSO: shrink unimportant coefficients <span style="color: red">(Least Absolute Shrinkage and Selection Operator)</span>

- LASSO adds an L1 penalty while fitting a linear model.
- It can shrink some feature coefficients exactly to zero.
- A zero coefficient means that feature is not used by that fitted model.

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; flex-direction:column; gap:20px; white-space:nowrap;">
    <div style="display:flex; align-items:center; gap:32px;">
      <div style="background:#f0f7fa; border-radius:24px; padding:24px 40px; box-shadow: 0 2px 6px #00000022; width: 320px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Haemoglobin</span>
      </div>
      <span style="font-size:30px; font-weight:700; color:#008b94;">0.72</span>
    </div>
    <div style="display:flex; align-items:center; gap:32px;">
      <div style="background:#f0f7fa; border-radius:24px; padding:24px 40px; box-shadow: 0 2px 6px #00000022; width: 320px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Blood pressure</span>
      </div>
      <span style="font-size:30px; font-weight:700; color:#008b94;">0.31</span>
    </div>
    <div style="display:flex; align-items:center; gap:32px;">
      <div style="background:#f0f7fa; border-radius:24px; padding:24px 40px; box-shadow: 0 2px 6px #00000022; width: 320px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Patient ID</span>
      </div>
      <span style="font-size:30px; font-weight:700; color:#008b94;">0.00</span>
    </div>
  </div>
</div>

In a linear model, each feature has a <mark>coefficient</mark>. This coefficient represents how that feature contributes to the model's prediction, while the other features are held constant.

> LASSO applies L1 regularisation to a linear model by adding a penalty to the size of its coefficients. As the penalty becomes stronger, some coefficients may become exactly zero, effectively excluding those features from the fitted model. The result depends on the penalty strength and data.

### LASSO: a simple example

Suppose we predict CKD using four candidate features.

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; flex-direction:column; gap:20px; white-space:nowrap;">
    <div style="display:flex; align-items:center; gap:60px;">
      <div style="background:#f0f7fa; border-radius:24px; padding:12px 20px; box-shadow: 0 2px 6px #00000022; width: 420px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Haemoglobin</span>
      </div>
      <div style="background:#e0f7f9; border-radius:24px; padding:12px 20px; box-shadow: 0 2px 6px #00000022; width: 320px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Keep</span>
      </div>
    </div>
    <div style="display:flex; align-items:center; gap:60px;">
      <div style="background:#f0f7fa; border-radius:24px; padding:12px 20px; box-shadow: 0 2px 6px #00000022; width: 420px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Blood pressure</span>
      </div>
      <div style="background:#e0f7f9; border-radius:24px; padding:12px 20px; box-shadow: 0 2px 6px #00000022; width: 320px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Keep</span>
      </div>
    </div>
    <div style="display:flex; align-items:center; gap:60px;">
      <div style="background:#f0f7fa; border-radius:24px; padding:12px 20px; box-shadow: 0 2px 6px #00000022; width: 420px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Age</span>
      </div>
      <div style="background:#e0f7f9; border-radius:24px; padding:12px 20px; box-shadow: 0 2px 6px #00000022; width: 320px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">May keep</span>
      </div>
    </div>
    <div style="display:flex; align-items:center; gap:60px;">
      <div style="background:#f0f7fa; border-radius:24px; padding:12px 20px; box-shadow: 0 2px 6px #00000022; width: 420px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Random ID</span>
      </div>
      <div style="background:#ffe9c8; border-radius:24px; padding:12px 20px; box-shadow: 0 2px 6px #00000022; width: 320px; display:flex; justify-content:center;">
        <span style="font-size:24px; font-weight:600; color:#222d38;">Remove</span>
      </div>
    </div>
  </div>
</div>

> Consider a CKD prediction task with haemoglobin, blood pressure, age, and a random patient identifier. An L1-regularised model might retain the medically informative measurements while assigning the identifier a coefficient of zero. This is an illustration; real results must be learned from the training data.

<span style="color: #5D6E7D">Illustration only: the real selected features depend on the data and penalty strength.</span>

Emphasise that the algorithm decides from training data, and a different dataset or regularisation setting may lead to different selected features.

## RFE: remove features step by step

> Recursive Feature Elimination (RFE) is a wrapper method that repeatedly fits a model and removes the least important feature or features. The process continues until the required number of features remains. The final selection depends on the estimator and its importance ranking.

- Start with all candidate features.
- Fit a model and rank feature importance.
- Remove the least important feature(s).
- Repeat until the desired number remains.

It needs a model capable of ranking feature importance or coefficients, and it may take more computation than a filter method.

### RFE: worked classroom example

> Imagine that a CKD dataset contains five candidate features and we want to retain only two. RFE first trains a model using all five, removes the lowest-ranked feature, and repeats this process. The two remaining features are selected according to the fitted model’s rankings.

Goal: keep 2 of 5 features (illustrative).

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:12px; align-items:center; white-space:nowrap;">
    <div style="background:#F2F7F9; border-radius:24px; padding:16px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
      <span style="font-size:24px; font-weight:600; color:#222d38;">Age  •  BP  •  Haemoglobin  •  Patient ID  •  Sugar</span>
    </div>
  </div>
</div>

<span style="color: #008B95"><b>↓ Remove Patient ID</b></span>

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:12px; align-items:center; white-space:nowrap;">
    <div style="background:#F2F7F9; border-radius:24px; padding:16px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
      <span style="font-size:24px; font-weight:600; color:#222d38;">Age  •  BP  •  Haemoglobin  •  Sugar</span>
    </div>
  </div>
</div>

<span style="color: #008B95"><b>↓ Continue ranking and removing</b></span>

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:12px; align-items:center; white-space:nowrap;">
    <div style="background:#DDF4F3; border-radius:24px; padding:16px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
      <span style="font-size:24px; font-weight:600; color:#222d38;">Haemoglobin  •  Sugar</span>
    </div>
  </div>
</div>

## Boruta: compare with random features

> Boruta is a feature selection method that compares the importance of original features with randomly shuffled copies called shadow features. A tree-based model is used to estimate importance. Features that consistently perform better than the random references are considered relevant.

- Create shuffled copies of the real features (“shadow features”).
- Train a tree-based model to measure feature importance.
- Compare real features with the shadow features.
- Keep features that consistently outperform random noise.

### Boruta: easy analogy

> Boruta can be understood as a competition between real measurements and randomised versions of those measurements. If haemoglobin consistently provides more useful information than shuffled shadow features, it has evidence of relevance. This comparison is repeated to make the decision more reliable.

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; align-items:center; gap:40px; white-space:nowrap;">
    <div style="background:#e0f7f9; border-radius:24px; padding:24px 60px; box-shadow: 0 2px 6px #00000022; display:flex; justify-content:center;">
      <span style="font-size:24px; font-weight:600; color:#222d38;">Real feature: Haemoglobin</span>
    </div>
    <div style="background:#f2f7f9; border-radius:24px; padding:24px 60px; box-shadow: 0 2px 6px #00000022; display:flex; justify-content:center;">
      <span style="font-size:24px; font-weight:600; color:#222d38;">Shadow feature: shuffled values</span>
    </div>
  </div>
</div>

If the real feature consistently performs better than random shadows, Boruta considers it relevant.

Imagine a competition between real students and randomly guessing students.

## LASSO vs RFE vs Boruta

| Method | Basic idea                            | Typical strength         |
| ------ | ------------------------------------- | ------------------------ |
| LASSO  | Shrink some coefficients to zero      | Efficient, interpretable |
| RFE    | Repeatedly remove low-ranked features | Controls number selected |
| Boruta | Beat shuffled shadow features         | Finds relevant features  |

> No single method is always best. LASSO, RFE, and Boruta use different criteria for selecting features. LASSO relies on coefficient shrinkage, RFE eliminates low-ranked features iteratively, and Boruta tests relevance against random shadow features. Consequently, the methods may produce different subsets on the same dataset.

<span style="color: #5D6E7D">Different methods may choose different features — compare their results.</span>

## Machine Learning Workflow with Feature Selection

1. Split train / test - Divide the dataset into training and testing sets.
2. Feature Scaling — Fit the scaler on the training data and transform both sets
3. SMOTE / SVMSMOTE — Balance the training data only.
4. Feature Selection — Apply LASSO, RFE, or Boruta to the balanced training data.
5. Model Training — Train the machine learning model using the selected features.
6. Model Evaluation — Evaluate performance using the original test samples with the same scaling and selected features.

> Feature selection is performed after data splitting, scaling, and SMOTE in this practical workflow. The feature selection method is fitted using only the training data, and the selected features are subsequently applied to the test data. This prevents data leakage and ensures that model performance is evaluated on previously unseen samples.

<span style="color: #5D6E7D">During cross-validation, selection must be repeated inside each training fold.</span>

## CKD Practical: What Will We Compare

> Suppose KNN achieves 100% accuracy using 24 features, while KNN with RFE achieves 100% accuracy using only 10 features. Which model would you prefer, and why?

## Quick class exercise

You have these columns:

<div style="overflow-x:auto; padding: 10px 0;">
  <div style="display:flex; gap:12px; align-items:center; white-space:nowrap;">
    <div style="background:#F2F7F9; border-radius:24px; padding:16px 40px; box-shadow: 0 2px 6px #00000022; text-align:center;">
      <span style="font-size:24px; font-weight:600; color:#222d38;">Patient ID  •  Age  •  Blood pressure  •  Haemoglobin  •  Sugar</span>
    </div>
  </div>
</div>

- Which column would you remove first, and why?
- Why might LASSO and RFE choose different features?
- Does fewer features always mean better accuracy?

> The purpose of feature selection is not simply to remove as many features as possible. It is to identify a useful subset of features that allows the model to achieve good predictive performance while reducing unnecessary complexity.

## Key takeaways

- Feature selection keeps useful existing variables.
- Filter, wrapper and embedded methods take different approaches.
- LASSO shrinks coefficients; RFE eliminates features; Boruta compares with random shadows.
- Select features using training data only — then evaluate fairly.

> Feature selection aims to identify a useful subset of original input variables while maintaining reliable predictive performance. LASSO, RFE, and Boruta provide three different ways to achieve this goal. In the next practical session, students will apply these methods to CKD data and compare the results.

<span style="color: #008B95"><b>Next: apply LASSO, RFE and Boruta to the CKD dataset.</b></span>

### Which Feature Selection Method

A. Remove features by shrinking their coefficients to zero

B. Repeatedly eliminate the least important features using a trained model

C. Compare real features against randomly shuffled features

---

Why can removing highly correlated features be beneficial in machine learning?

---

### LASSO: interpret the coefficients

LASSO uses L1 regularisation to reduce the size of model coefficients. When a coefficient becomes exactly zero, its corresponding feature is excluded from the model. The strength of regularisation controls how aggressively coefficients are reduced. For classification, L1-regularised logistic regression is a common implementation.

### RFE: choosing how many features to retain

Recursive Feature Elimination begins with a fitted estimator, ranks features by their contribution, removes the least important feature or features, and repeats this process until a chosen number remains. The ranking depends on the estimator and the training data. The number of retained features is a design choice that should be evaluated.

::: info PAIR DISCUSSION
Pair discussion: If RFE starts with 8 features and removes 2 per round until 2 remain, how many elimination rounds are needed? What could change if the estimator changes?
:::

### Boruta: why use shadow features

Boruta adds randomly shuffled copies of the original features, known as shadow features. A tree-based model estimates feature importance, and original features are compared against the randomised benchmarks over repeated trials. This helps identify variables that show evidence of relevance, rather than simply selecting a fixed number of features.

::: info PAIR DISCUSSION
Discuss: If a real feature performs no better than its shuffled version, what does this suggest? Why might the conclusion vary between runs?
:::

### Pair activity: choose a selection method

Consider three research goals:  
(A) identify a compact set of predictors using a linear model;  
(B) retain exactly five features based on a chosen classifier;  
(C) identify all features that appear relevant compared with randomised features. Each goal favours a different selection strategy.  

::: info PAIR DISCUSSION
- Match A, B, and C to LASSO, RFE, or Boruta.
- Explain your reasoning to your partner before revealing your answers.
:::

### Live poll: check your understanding

::: info POLL
Which method repeatedly removes low-ranked features?  A. LASSO  B. RFE  C. Boruta  D. StandardScaler
:::

### Live poll: compare the three methods

LASSO, RFE, and Boruta differ in their selection mechanisms. LASSO shrinks coefficients, RFE removes features based on an estimator’s rankings, and Boruta compares real features with shuffled shadow features. There is no single method that is guaranteed to perform best on every dataset.

::: info MENTIMETER POLL
Rank LASSO, RFE, and Boruta by which you would try first for the CKD project, then discuss your reasoning. There is no single correct ranking.
:::

Source: [week4featureselection.pptx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fweek4featureselection.pptx&wdOrigin=BROWSELINK)
