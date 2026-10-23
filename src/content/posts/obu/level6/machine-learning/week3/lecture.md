---
title: "Supervised Learning, Training & Testing, Model Evaluation and Classification (I)"
published: 2026-10-20
publishedAt: 2026-10-20T16:25:00+08:00
description: "Explain supervised classification and the roles of features and labels; Illustrate a train–test split and the importance of unseen test data; Describe how Logistic Regression and KNN make predictions; Interpret a confusion matrix and calculate accuracy, precision, recall and F1-score."
image: "./151042504.png"
tags: ["Supervised Learning", "Training", "Testing", "Model Evaluation", "Classification"]
category: "Machine Learning"
draft: false
pinned: false
lang: en
---

## Learning outcomes

- Explain supervised classification and the roles of features and labels.
- Illustrate a train–test split and the importance of unseen test data.
- Describe how Logistic Regression and KNN make predictions.
- Interpret a confusion matrix and calculate accuracy, precision, recall and F1-score.

## Where Week 3 fits

<span style="color: gray">From prepared data to trustworthy model evaluation</span>

- Week 1: Machine learning concepts and the ML workflow.
- Week 2: Data preprocessing and exploratory data analysis.
- Week 3: Train/test, classification models and evaluation.
- Week 4: Feature selection (LASSO, RFE and Boruta).

## The supervised classification workflow

```mermaid
graph LR
    A["Labeled data"] --> B["Prepare data"]
    B --> C["Train/test split"]
    C --> D["Fit classifier"]:::highlight
    D --> E["Predict test labels"]
    E --> F["Evaluate"]
    
    classDef highlight fill:#009696,color:#ffffff
```

<center><span style="color: #2065B4">The <mark>test</mark> set is reserved for the final assessment of generalisation.</span></center>

## What is supervised learning?

<div style="display: flex; gap: 12px; overflow-x: auto; width: 100%;">
  <!-- Left panel: Inputs X (features) -->
  <div style="flex: 1; min-width: 400px; background-color: #f0f6fd; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #2468b8; margin-top:0; font-size: 2.0rem; font-weight: bold;">Inputs: X (features)</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Measurable information about each example.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Animal image: visual characteristics.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Patient dataset: age, blood pressure, laboratory values.</p>
  </div>
  <!-- Right panel: Output y (label) -->
  <div style="flex: 1; min-width: 400px; background-color: #eaf8f5; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #189c94; margin-top:0; font-size: 2.0rem; font-weight: bold;">Output: y (label)</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Known target associated with each training example.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Animal image: cat or dog.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Patient dataset: CKD or not CKD.</p>
  </div>
</div>

## Quick check

<center><h3>Which is the target variable in a dataset predicting chronic kidney disease?</h3></center>

<center><span style="color: grey">Think individually • Discuss with a partner • Explain your reasoning</span></center>

## Why split a dataset

<div style="display: flex; gap: 12px; overflow-x: auto; width: 100%;">
  <!-- Left panel: Training set -->
  <div style="flex: 1; min-width: 400px; background-color: #f0f6fd; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #2468b8; margin-top:0; font-size: 2.0rem; font-weight: bold;">Training set</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Examples used to learn relationships between X and y.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">The algorithm may see their labels while fitting.</p>
  </div>
  <!-- Right panel: Test set -->
  <div style="flex: 1; min-width: 400px; background-color: #eaf8f5; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #189c94; margin-top:0; font-size: 2.0rem; font-weight: bold;">Test set</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Held-out examples used to estimate performance on new, unseen cases.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Do not fit the model using these examples.</p>
  </div>
</div>

### Example: an 80/20 train–test split

100 labelled observations

<div style="display: flex; width:100%; overflow-x:auto;">
  <div style="width:80%; min-width: 400px; background-color:#2468b8; display:flex; align-items:center; justify-content:center; padding:40px 0;">
    <span style="color:white; font-size:1.5rem; font-weight:bold;">80 training observations</span>
  </div>
  <div style="width:20%; min-width: 100px; background-color:#189c94; display:flex; align-items:center; justify-content:center; padding:40px 0;">
    <span style="color:white; font-size:1.5rem; font-weight:bold;">20 test</span>
  </div>
</div>

<span style="color: grey">The 80/20 ratio is common, not mandatory. Choose a split appropriate to the data.</span>

## Prediction before the demonstration

<center><h3>If you memorises every training photograph, will you necessarily recognise a new photograph of the same animal?</h3></center>

<center><span style="color: grey">Think individually • Discuss with a partner • Explain your reasoning</span></center>

## Activity: a student becomes the classifier

<span style="color: grey">Interactive learning</span>

- One volunteer to be the “model”; participation is optional.
- Show labelled examples from two familiar animal categories.
- Ask classmates to identify the visual clues that distinguish categories.
- Keep the test photographs hidden until prediction time.

## Demonstration: training vs unseen testing

<div style="display: flex; gap: 12px; overflow-x: auto; width: 100%;">
  <!-- Left panel: TRAINING -->
  <div style="flex: 1; min-width: 400px; background-color: #f0f6fd; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #2468b8; margin-top:0; font-size: 2.0rem; font-weight: bold;">TRAINING</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Show labelled photographs<br>CAT • DOG</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Volunteer learns distinguishing patterns.</p>
  </div>
  <!-- Right panel: TESTING -->
  <div style="flex: 1; min-width: 400px; background-color: #eaf8f5; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #189c94; margin-top:0; font-size: 2.0rem; font-weight: bold;">TESTING</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Show NEW photographs<br>Labels hidden</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Volunteer predicts; classmates vote; <br>reveal answers.</p>
  </div>
</div>

![](img/Pasted_image_20261020210214.png)

### Test set

![](img/Pasted_image_20261020210324.png)
![](img/Pasted_image_20261020210329.png)
![](img/Pasted_image_20261020210333.png)
![](img/Pasted_image_20261020210337.png)
![](img/Pasted_image_20261020210341.png)
![](img/Pasted_image_20261020210346.png)
![](img/Pasted_image_20261020210351.png)
![](img/Pasted_image_20261020210359.png)
![](img/Pasted_image_20261020210403.png)
![](img/Pasted_image_20261020210407.png)

### Discussion

<center><h3>What if we show the model unfamiliar animals?</h3></center>

<center><span style="color: grey">Think individually • Discuss with a partner • Explain your reasoning</span></center>

![](img/Pasted_image_20261020210700.png)

### Discussion

<center><h3>Limitation of the model when it encounters unfamiliar data</h3></center>

<center><span style="color: grey">Think individually • Discuss with a partner • Explain your reasoning</span></center>

### Discussion

<center><h3>What did the Model(volunteer) learn: individual pictures or characteristics that transfer to new pictures?</h3></center>

<center><span style="color: grey">Think individually • Discuss with a partner • Explain your reasoning</span></center>

## Memorisation vs generalisation

<div style="display: flex; gap: 12px; overflow-x: auto; width: 100%;">
  <!-- Left panel: Memorisation / overfitting -->
  <div style="flex: 1; min-width: 450px; background-color: #f0f6fd; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #2468b8; margin-top:0; font-size: 2.0rem; font-weight: bold;">Memorisation / overfitting</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Excellent performance on examples already seen.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">May rely on irrelevant details, backgrounds or coincidences.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Can perform poorly on unseen examples.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Memorisation means remembering specific training examples instead of learning general patterns. A model might recognise photographs it has already seen but struggle with new photographs</p>
  </div>
  <!-- Right panel: Generalisation -->
  <div style="flex: 1; min-width: 450px; background-color: #eaf8f5; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #189c94; margin-top:0; font-size: 2.0rem; font-weight: bold;">Generalisation</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Learns useful patterns that transfer to new observations.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Performance remains reasonably strong on held-out test data.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">The ability of a machine learning model to make accurate predictions on new, unseen data</p>
  </div>
</div>

## Memorisation vs generalisation vs overfitting

| Concept        | Description                                                         | Example                                                     |
| -------------- | ------------------------------------------------------------------- | ----------------------------------------------------------- |
| Memorisation   | Remembering specific examples                                       | Recognising the same cat photograph shown during training   |
| Generalisation | Applying learned patterns to new examples                           | Correctly recognising a different cat photograph            |
| Overfitting    | Fitting training data too closely and performing poorly on new data | Very high training accuracy but much lower testing accuracy |

## Think–pair–share

<center><h3>A model scores 99% on training data but 65% on test data. What might explain the gap?</h3></center>

<center><span style="color: grey">Think individually • Discuss with a partner • Explain your reasoning</span></center>

## Data leakage: why evaluation can be misleading

Leakage occurs when information unavailable at prediction time influences model development.

<div style="display: flex; gap:12px; overflow-x:auto; width:100%;">
  <!-- Example 1 -->
  <div style="flex:1; min-width:350px; background-color:#f0f6fd; padding:40px 24px; box-sizing:border-box;">
    <h2 style="color:#2468b8; margin:0 0 2rem 0; font-size:1.5rem; font-weight:bold;">Example 1</h2>
    <p style="font-size:1rem; color:#222; margin:0;">Scaling fitted on all data</p>
  </div>
  <!-- Example 2 -->
  <div style="flex:1; min-width:350px; background-color:#eaf8f5; padding:40px 24px; box-sizing:border-box;">
    <h2 style="color:#2468b8; margin:0 0 2rem 0; font-size:1.5rem; font-weight:bold;">Example 2</h2>
    <p style="font-size:1rem; color:#222; margin:0;">SMOTE before splitting</p>
  </div>
  <!-- Example 3 -->
  <div style="flex:1; min-width:350px; background-color:#f0f6fd; padding:40px 24px; box-sizing:border-box;">
    <h2 style="color:#2468b8; margin:0 0 2rem 0; font-size:1.5rem; font-weight:bold;">Example 3</h2>
    <p style="font-size:1rem; color:#222; margin:0;">Selecting features using test labels</p>
  </div>
</div>

<span style="color: #008F96">Safer sequence: split first → fit preprocessing on training data → transform test data.</span>

## Train–test split: important considerations

- Shuffle observations when appropriate; respect time order for time-series data.
- For imbalanced classification, consider stratified splitting to preserve class proportions.
- Use a fixed random state for reproducible demonstrations.
- Keep the test set separate from training and model selection.

## Model training and prediction

<div style="display: flex; gap:12px; overflow-x:auto; width:100%;">
  <!-- FIT -->
  <div style="flex:1; min-width:300px; background-color:#f0f6fd; padding:40px 24px; box-sizing:border-box; text-align:center;">
    <h2 style="color:#2468b8; margin:0 0 2rem 0; font-size:2rem; font-weight:bold;">FIT</h2>
    <p style="font-size:1rem; color:#222; margin:0;">The classifier learns from<br>X_train and y_train.</p>
  </div>
  <!-- PREDICT -->
  <div style="flex:1; min-width:300px; background-color:#f0f6fd; padding:40px 24px; box-sizing:border-box; text-align:center;">
    <h2 style="color:#2468b8; margin:0 0 2rem 0; font-size:2rem; font-weight:bold;">PREDICT</h2>
    <p style="font-size:1rem; color:#222; margin:0;">The fitted classifier<br>receives X_test.</p>
  </div>
  <!-- COMPARE -->
  <div style="flex:1; min-width:300px; background-color:#f0f6fd; padding:40px 24px; box-sizing:border-box; text-align:center;">
    <h2 style="color:#2468b8; margin:0 0 2rem 0; font-size:2rem; font-weight:bold;">COMPARE</h2>
    <p style="font-size:1rem; color:#222; margin:0;">Predicted labels are<br>compared with y_test.</p>
  </div>
</div>

## Classification I: two different approaches

- Logistic Regression: learns a decision boundary and estimates class probabilities.
- K-Nearest Neighbors (KNN): predicts using nearby labelled examples.
- Both are supervised classifiers, but they make predictions differently.

## Logistic Regression: the intuition

| <span style="color: #2065B4"><b>Input features</b></span> |                                       | <span style="color: #2065B4"><b>Weighted score</b></span> |                                       | <span style="color: #008F96"><b>Probability</b></span> |
| --------------------------------------------------------- | ------------------------------------- | --------------------------------------------------------- | ------------------------------------- | ------------------------------------------------------ |
| $X_1,X_2,\dots,X_n$                                       | <span style="color: #008F96">→</span> | $z = b + \sum w_i x_i$                                    | <span style="color: #008F96">→</span> | $P(y=1 \vert X)$                                       |

<span style="color: grey">The sigmoid function converts a score into a value between 0 and 1.</span>

## Logistic Regression: sigmoid function

$\sigma(z) = \frac{1}{1 + e^{-z}}$

P ≥ 0.5 → predict positive  
P < 0.5 → predict negative

Threshold can be adjusted.

![](img/Pasted_image_20261020212955.png)

## Logistic Regression: concept check

<center><h3>A classifier estimates P(CKD) = 0.82. With a 0.50 decision threshold, what label does it predict?</h3>Logistic Regression produces a probability, and the decision threshold converts that probability into a class label</center>

<center><span style="color: grey">Think individually • Discuss with a partner • Explain your reasoning</span></center>

## KNN: classify by nearby examples

1. Choose K (number of neighbors).
2. Measure distances to labelled training examples.
3. Find the K closest examples.
4. Use majority vote for classification.

![](img/Pasted_image_20261020213249.png)

## KNN: choosing K

<div style="display: flex; gap: 12px; overflow-x: auto; width: 100%;">
  <!-- Small K -->
  <div style="flex: 1; min-width: 350px; background-color: #f0f6fd; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #2468b8; margin-top:0; font-size: 2.0rem; font-weight: bold;">Small K</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Sensitive to local patterns and noise.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">K = 1 may overfit.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Prediction can change when a single neighbor changes.</p>
  </div>
  <!-- Large K -->
  <div style="flex: 1; min-width: 350px; background-color: #eaf8f5; padding: 32px; border-radius: 8px; box-sizing: border-box;">
    <h2 style="color: #189c94; margin-top:0; font-size: 2.0rem; font-weight: bold;">Large K</h2>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Smoother decision boundaries.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">May overlook local patterns.</p>
    <p style="font-size: 1.0rem; color: #222222; line-height: 1.6;">Very large K can underfit.</p>
  </div>
</div>

## KNN: majority vote

<center><h3>For K = 5, the nearest labels are [Cat, Dog, Cat, Cat, Dog]. <br>What is the prediction?</h3></center>

<center><span style="color: grey">Think individually • Discuss with a partner • Explain your reasoning</span></center>

<div style="background:#000; padding:24px; border-radius:16px; overflow-x:auto;">
  <!-- 统一横向滚动容器：上下内容共用这个宽度 -->
  <div style="display:inline-block; min-width:100%;">
    <!-- 第一排：5个卡片 -->
    <div style="display:flex; gap:16px; margin-bottom:32px;">
      <!-- Cat #1 -->
      <div style="background:#0a1020; flex:1; min-width:160px; padding:24px 12px; border-radius:12px; text-align:center;">
        <div style="font-size:24px; color:#4285f4;">🐱</div>
        <div style="color:#fff; font-size:16px; margin:8px 0 4px;">Cat</div>
        <div style="color:#fff; font-size:14px;">#1</div>
      </div>
      <!-- Dog #2 -->
      <div style="background:#281810; flex:1; min-width:160px; padding:24px 12px; border-radius:12px; text-align:center;">
        <div style="font-size:24px; color:#ffd045;">🐶</div>
        <div style="color:#fff; font-size:16px; margin:8px 0 4px;">Dog</div>
        <div style="color:#fff; font-size:14px;">#2</div>
      </div>
      <!-- Cat #3 -->
      <div style="background:#0a1020; flex:1; min-width:160px; padding:24px 12px; border-radius:12px; text-align:center;">
        <div style="font-size:24px; color:#4285f4;">🐱</div>
        <div style="color:#fff; font-size:16px; margin:8px 0 4px;">Cat</div>
        <div style="color:#fff; font-size:14px;">#3</div>
      </div>
      <!-- Cat #4 -->
      <div style="background:#0a1020; flex:1; min-width:160px; padding:24px 12px; border-radius:12px; text-align:center;">
        <div style="font-size:24px; color:#4285f4;">🐱</div>
        <div style="color:#fff; font-size:16px; margin:8px 0 4px;">Cat</div>
        <div style="color:#fff; font-size:14px;">#4</div>
      </div>
      <!-- Dog #5 -->
      <div style="background:#281810; flex:1; min-width:160px; padding:24px 12px; border-radius:12px; text-align:center;">
        <div style="font-size:24px; color:#ffd045;">🐶</div>
        <div style="color:#fff; font-size:16px; margin:8px 0 4px;">Dog</div>
        <div style="color:#fff; font-size:14px;">#5</div>
      </div>
    </div>
    <!-- 第二排：与上排同总宽度，左右严格对半分 -->
    <div style="display:flex;">
      <div style="flex:1; text-align:center;">
        <div style="color:#4285f4; font-size:32px; font-weight:bold;">3</div>
        <div style="color:#fff; font-size:20px;">Cats</div>
      </div>
      <div style="flex:1; text-align:center;">
        <div style="color:#fff; font-size:32px; font-weight:bold;">2</div>
        <div style="color:#fff; font-size:20px;">Dogs</div>
      </div>
    </div>
  </div>
</div>

## Logistic Regression vs KNN

<div style="display:flex; gap:24px; overflow-x:auto; width:100%; box-sizing:border-box;">
  <!-- Logistic Regression -->
  <div style="flex:1; min-width:400px; background:#f0f6fd; padding:32px; border:1px solid #e5e7eb; border-radius:8px;">
    <h2 style="color:#2468b8; font-size:2.0rem; margin:0 0 32px 0; font-weight:bold;">Logistic Regression</h2>
    <p style="font-size:1.0rem; color:#222; line-height:1.7; margin:0 0 24px 0;">Learns coefficients during training.</p>
    <p style="font-size:1.0rem; color:#222; line-height:1.7; margin:0 0 24px 0;">Often efficient at prediction.</p>
    <p style="font-size:1.0rem; color:#222; line-height:1.7; margin:0 0 24px 0;">Produces estimated class probabilities.</p>
    <p style="font-size:1.0rem; color:#222; line-height:1.7; margin:0;">Typically a linear decision boundary.</p>
  </div>
  <!-- K-Nearest Neighbors -->
  <div style="flex:1; min-width:400px; background:#eaf8f5; padding:32px; border:1px solid #e5e7eb; border-radius:8px;">
    <h2 style="color:#189c94; font-size:2.0rem; margin:0 0 32px 0; font-weight:bold;">K-Nearest Neighbors</h2>
    <p style="font-size:1.0rem; color:#222; line-height:1.7; margin:0 0 24px 0;">Stores labelled examples.</p>
    <p style="font-size:1.0rem; color:#222; line-height:1.7; margin:0 0 24px 0;">Prediction uses distance and voting.</p>
    <p style="font-size:1.0rem; color:#222; line-height:1.7; margin:0 0 24px 0;">Sensitive to feature scale.</p>
    <p style="font-size:1.0rem; color:#222; line-height:1.7; margin:0;">Can model nonlinear boundaries.</p>
  </div>
</div>

## Why scaling matters especially for KNN

<span style="color: grey">Recall from Week 2; practical implementation belongs in the seminar</span>

- KNN depends on distances between observations.
- A feature with a large numeric range may dominate Euclidean distance.
- StandardScaler can help place numeric features on comparable scales.
- Fit the scaler on training data only; apply the learned transform to the test data.

## From predictions to evaluation

| <span style="color: #2065B4"><b>Actual labels</b></span> |     | <span style="color: #008F96"><b>Predicted labels</b></span> |
| -------------------------------------------------------- | --- | ----------------------------------------------------------- |
| 1, 0, 1, 1, 0, 0                                         |     | 1, 0, 0, 1, 1, 0                                            |

Count correct and incorrect predictions—then identify the TYPES of error.

## Confusion matrix: four possible outcomes

<div style="width:100%; overflow-x:auto; box-sizing:border-box;">
  <div style="display:grid; grid-template-columns: 1fr 1fr; gap:24px; min-width:600px;">
    <!-- TP True Positive -->
    <div style="background:#f0f6fd; padding:24px; border-left:8px solid #27a262; border-radius:4px; box-shadow:0 2px 4px #00000020; display:flex; align-items:center; gap:24px;">
      <div style="font-size:2rem; font-weight:bold; color:#27a262;">TP</div>
      <div>
        <div style="font-size:1.2rem; font-weight:bold; color:#1a2440;">TRUE POSITIVE</div>
        <div style="font-size:1.0rem; color:#707886; margin-top:12px;">Correct positive</div>
      </div>
    </div>
    <!-- FN False Negative -->
    <div style="background:#f0f6fd; padding:24px; border-left:8px solid #d64848; border-radius:4px; box-shadow:0 2px 4px #00000020; display:flex; align-items:center; gap:24px;">
      <div style="font-size:2rem; font-weight:bold; color:#d64848;">FN</div>
      <div>
        <div style="font-size:1.2rem; font-weight:bold; color:#1a2440;">FALSE NEGATIVE</div>
        <div style="font-size:1.0rem; color:#707886; margin-top:12px;">Missed positive</div>
      </div>
    </div>
    <!-- FP False Positive -->
    <div style="background:#f0f6fd; padding:24px; border-left:8px solid #d64848; border-radius:4px; box-shadow:0 2px 4px #00000020; display:flex; align-items:center; gap:24px;">
      <div style="font-size:2rem; font-weight:bold; color:#d64848;">FP</div>
      <div>
        <div style="font-size:1.2rem; font-weight:bold; color:#1a2440;">FALSE POSITIVE</div>
        <div style="font-size:1.0rem; color:#707886; margin-top:12px;">False alarm</div>
      </div>
    </div>
    <!-- TN True Negative -->
    <div style="background:#f0f6fd; padding:24px; border-left:8px solid #27a262; border-radius:4px; box-shadow:0 2px 4px #00000020; display:flex; align-items:center; gap:24px;">
      <div style="font-size:2rem; font-weight:bold; color:#27a262;">TN</div>
      <div>
        <div style="font-size:1.2rem; font-weight:bold; color:#1a2440;">TRUE NEGATIVE</div>
        <div style="font-size:1.0rem; color:#707886; margin-top:12px;">Correct negative</div>
      </div>
    </div>
  </div>
</div>

## Worked example: confusion matrix (100 patients)

<div style="width:100%; overflow-x:auto; box-sizing:border-box;">
  <div style="display:grid; grid-template-columns: 220px 1fr 1fr; gap:24px; min-width:300px; align-items:stretch;">
    <!-- 顶部空白占位 -->
    <div></div>
    <div style="text-align:center; font-size:1.0rem; font-weight:bold; color:#2468b8; padding-bottom:16px;">Predicted CKD</div>
    <div style="text-align:center; font-size:1.0rem; font-weight:bold; color:#2468b8; padding-bottom:16px;">Predicted not CKD</div>
    <!-- 第一行 Actual CKD -->
    <div style="display:flex; align-items:center; font-size:1.0rem; font-weight:bold;">Actual CKD</div>
    <div style="background:#f0f6fd; box-shadow:0 2px 4px #00000020; border-radius:4px; display:flex; flex-direction:column; justify-content:center; align-items:center; padding:18px 20px;">
      <div style="font-size:2rem; font-weight:bold; color:#27a262;">30</div>
      <div style="font-size:1.0rem; color:#707886; margin-top:8px;">TP</div>
    </div>
    <div style="background:#f0f6fd; box-shadow:0 2px 4px #00000020; border-radius:4px; display:flex; flex-direction:column; justify-content:center; align-items:center; padding:18px 20px;">
      <div style="font-size:2rem; font-weight:bold; color:#d64848;">10</div>
      <div style="font-size:1.0rem; color:#707886; margin-top:8px;">FN</div>
    </div>
    <!-- 第二行 Actual not CKD -->
    <div style="display:flex; align-items:center; font-size:1.0rem; font-weight:bold;">Actual not CKD</div>
    <div style="background:#f0f6fd; box-shadow:0 2px 4px #00000020; border-radius:4px; display:flex; flex-direction:column; justify-content:center; align-items:center; padding:18px 20px;">
      <div style="font-size:2rem; font-weight:bold; color:#d64848;">5</div>
      <div style="font-size:1.0rem; color:#707886; margin-top:8px;">FP</div>
    </div>
    <div style="background:#f0f6fd; box-shadow:0 2px 4px #00000020; border-radius:4px; display:flex; flex-direction:column; justify-content:center; align-items:center; padding:18px 20px;">
      <div style="font-size:2rem; font-weight:bold; color:#27a262;">55</div>
      <div style="font-size:1.0rem; color:#707886; margin-top:8px;">TN</div>
    </div>
  </div>
</div>

<span style="color: grey">Positive class = CKD</span>

### Accuracy: overall correctness

$$
\begin{align}
\text{Accuracy} &= \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}} \\
      &= \frac{30 + 55}{100} \\
      &= 85\%
\end{align}
$$

<span style="color: red">Limitation: high accuracy can hide poor detection of a rare positive class.</span>

### Precision: when the model predicts positive

$$
\begin{align}
\text{Precision} &= \frac{\text{TP}}{\text{TP} + \text{FP}} \\
      &= \frac{30}{30 + 5} \\
      &\approx 85.7\%
\end{align}
$$

<span style="color: grey">Question: Of the patients predicted to have CKD, how many truly have CKD?</span>

### Recall: how many actual positives were found?

$$
\begin{align}
\text{Recall} &= \frac{\text{TP}}{\text{TP} + \text{FN}} \\
      &= \frac{30}{30 + 10} \\
      &= 75\%
\end{align}
$$

<span style="color: grey">Question: Of all patients who truly have CKD, how many did the model detect?</span>

### F1-score: balancing precision and recall

$$
\begin{align}
\text{F1} &= \frac{2 \times (\text{Precision} \times \text{Recall})}{\text{Precision} + \text{Recall}} \\
      &= \frac{2 \times (0.857 \times 0.750)}{0.857 + 0.750} \\
      &\approx 80\%
\end{align}
$$

<span style="color: grey">F1 is useful when both false positives and false negatives matter.</span>

### Metric comparison: one example, four views

<div style="width:100%; overflow-x:auto; box-sizing:border-box;">
  <div style="display:grid; grid-template-columns: 240px 180px 1fr; gap:12px 0px; min-width:800px;">
    <!-- Accuracy -->
    <div style="background:#f0f6fd; padding:28px 24px; border-radius:0px; display:flex; align-items:center; font-size:1rem; font-weight:bold; color:#1a2440;">Accuracy</div>
    <div style="background:#f0f6fd; padding:28px 24px; border-radius:0px; display:flex; align-items:center; justify-content:center; font-size:1rem; font-weight:bold; color:#009691;">85.0%</div>
    <div style="background:#f0f6fd; padding:28px 24px; border-radius:0px; display:flex; align-items:center; font-size:1rem; color:#1a2440;">Overall correct predictions</div>
    <!-- Precision -->
    <div style="background:#eaf8f5; padding:28px 24px; border-radius:0px; display:flex; align-items:center; font-size:1rem; font-weight:bold; color:#1a2440;">Precision</div>
    <div style="background:#eaf8f5; padding:28px 24px; border-radius:0px; display:flex; align-items:center; justify-content:center; font-size:1rem; font-weight:bold; color:#009691;">85.7%</div>
    <div style="background:#eaf8f5; padding:28px 24px; border-radius:0px; display:flex; align-items:center; font-size:1rem; color:#1a2440;">Reliability of positive predictions</div>
    <!-- Recall -->
    <div style="background:#f0f6fd; padding:28px 24px; border-radius:0px; display:flex; align-items:center; font-size:1rem; font-weight:bold; color:#1a2440;">Recall</div>
    <div style="background:#f0f6fd; padding:28px 24px; border-radius:0px; display:flex; align-items:center; justify-content:center; font-size:1rem; font-weight:bold; color:#009691;">75.0%</div>
    <div style="background:#f0f6fd; padding:28px 24px; border-radius:0px; display:flex; align-items:center; font-size:1rem; color:#1a2440;">Coverage of actual positives</div>
    <!-- F1-score -->
    <div style="background:#eaf8f5; padding:28px 24px; border-radius:0px; display:flex; align-items:center; font-size:1rem; font-weight:bold; color:#1a2440;">F1-score</div>
    <div style="background:#eaf8f5; padding:28px 24px; border-radius:0px; display:flex; align-items:center; justify-content:center; font-size:1rem; font-weight:bold; color:#009691;">80.0%</div>
    <div style="background:#eaf8f5; padding:28px 24px; border-radius:0px; display:flex; align-items:center; font-size:1rem; color:#1a2440;">Balance of precision and recall</div>
  </div>
</div>

### Why accuracy alone can mislead

<center><h3>A dataset contains 95 healthy patients and 5 patients with a disease. A model predicts “healthy” for everyone. What is its accuracy—and its recall for disease?</h3></center>

<center><span style="color: grey">Think individually • Discuss with a partner • Explain your reasoning</span></center>

## Choosing the right metric

- Accuracy: useful when classes and error costs are reasonably balanced.
- Precision: important when false alarms are costly.
- Recall: important when missed positives are costly.
- F1-score: summarises the precision–recall trade-off.
- Always explain which class is considered “positive”.

## Final knowledge check

1. Why must test data remain unseen?
2. How does KNN decide a class?
3. What does a false negative mean?
4. When might recall matter more than accuracy?

## Week 3: key takeaways

- Split data to estimate generalisation on unseen observations.
- Fit preprocessing and models using training data only.
- Logistic Regression estimates probabilities; KNN uses neighbor voting.
- A confusion matrix separates correct predictions from different errors.
- Accuracy, precision, recall and F1-score answer different questions.

## Coming next: Week 4 — Feature Selection

### Which features should a model learn from?

<div style="width:100%; overflow-x:auto; box-sizing:border-box;">
  <div style="display:grid; grid-template-columns: 1fr 1fr 1fr; gap:12px; min-width:800px;">
    <!-- LASSO -->
    <div style="background:#f0f6fd; padding:32px 24px; border-radius:4px; box-shadow:0 2px 4px #00000020; display:flex; flex-direction:column; justify-content:center;">
      <div style="font-size:1.2rem; font-weight:bold; color:#2468b8; margin-bottom:16px;">LASSO</div>
      <div style="font-size:1rem; color:#1a2440;">Coefficient shrinkage</div>
    </div>
    <!-- RFE -->
    <div style="background:#eaf8f5; padding:32px 24px; border-radius:4px; box-shadow:0 2px 4px #00000020; display:flex; flex-direction:column; justify-content:center;">
      <div style="font-size:1.2rem; font-weight:bold; color:#2468b8; margin-bottom:16px;">RFE</div>
      <div style="font-size:1rem; color:#1a2440;">Recursive elimination</div>
    </div>
    <!-- Boruta -->
    <div style="background:#f0f6fd; padding:32px 24px; border-radius:4px; box-shadow:0 2px 4px #00000020; display:flex; flex-direction:column; justify-content:center;">
      <div style="font-size:1.2rem; font-weight:bold; color:#2468b8; margin-bottom:16px;">Boruta</div>
      <div style="font-size:1rem; color:#1a2440;">Shadow-feature comparison</div>
    </div>
  </div>
</div>

<center><span style="color: grey">Bring questions from the Week 3 seminar and think about why irrelevant features may hurt model performance.</span></center>

Source: [week3mllecture.pptx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fweek3mllecture.pptx&wdOrigin=BROWSELINK)
