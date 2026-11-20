---
title: "Week 7 Lecture: Dimensionality Reduction"
published: 2026-11-17
publishedAt: 2026-11-17T16:25:00+08:00
description: "Dimensionality reduction techniques aim to reduce the number of features (dimensions) while retaining as much information as possible."
image: "./152040541.jpg"
tags: ["PCA", "Factor Analysis", "LDA"]
category: "Machine Learning"
draft: false
pinned: false
lang: en
---

## Introduction to Dimensionality Reduction Techniques

Dimensionality reduction techniques aim to reduce the number of features (dimensions) while retaining as much information as possible.

Why it matters:

- Simplifies models: Reducing dimensions helps create simpler, more interpretable models.
- Speeds up computation: Fewer dimensions result in faster training and evaluation times.
- Prevents Overfitting: Reducing the feature space can improve the model's ability to generalize to new data. 

When to use:

- When you have high-dimensional data (many features) that could be summarized or compressed.

## Orientation

### A practical roadmap for today

Three techniques, one central question: what information should we keep?

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display: flex; gap: 12px; min-width: max-content;">
    <!-- PCA Card -->
    <div style="width: 410px; border: 1px solid #e2e8f0; border-left: 6px solid #28a799; border-radius: 12px; padding: 20px; background: #ffffff;">
      <h2 style="margin:0 0 16px 0; color: #1a2b42;">01 PCA</h2>
      <p style="color: #4a5568; line-height: 1.6;">Keep the directions where the data vary the most.</p>
      <p style="color: #4a5568; line-height: 1.6; margin-top: 24px;">Unsupervised feature extraction.</p>
    </div>
    <!-- Factor Analysis Card -->
    <div style="width: 400px; border: 1px solid #e2e8f0; border-left: 6px solid #3468a3; border-radius: 12px; padding: 20px; background: #ffffff;">
      <h2 style="margin:0 0 16px 0; color: #1a2b42;">02 Factor Analysis</h2>
      <p style="color: #4a5568; line-height: 1.6;">Find hidden factors that may explain correlations among observed features.</p>
      <p style="color: #4a5568; line-height: 1.6; margin-top: 24px;">Unsupervised latent-variable model.</p>
    </div>
    <!-- LDA Card -->
    <div style="width: 400px; border: 1px solid #e2e8f0; border-left: 6px solid #f2b138; border-radius: 12px; padding: 20px; background: #ffffff;">
      <h2 style="margin:0 0 16px 0; color: #1a2b42;">03 LDA</h2>
      <p style="color: #4a5568; line-height: 1.6;">Find a direction that separates known classes.</p>
      <p style="color: #4a5568; line-height: 1.6; margin-top: 24px;">Supervised feature extraction.</p>
    </div>
  </div>
</div>

<div style="border-radius: 16px; background-color: #dcf3ee; border-left: 6px solid #28a799; overflow: hidden;">
    <p style="margin: 0; padding: 18px 22px; color: #1a2b42;"><b>End goal: compare all features with reduced features using the SAME classifier and fair validation.</b></p>
</div>

## Warm-Up

### A dataset with 24 columns. Do we need all 24

Our familiar Chronic Kidney Disease classification example.

<div style="overflow-x: auto; padding: 16px 0;">
  <div style="display: flex; align-items: center; gap: 32px; min-width: max-content;">
    <!-- Left part: 24 original CKD predictors -->
    <div style="text-align: center; flex-shrink: 0;">
      <div style="font-size: 80px; font-weight: 700; color: #112236; line-height: 1;">24</div>
      <div style="color: #6b7280; margin-top: 8px;">original CKD predictors</div>
    </div>
    <!-- Green arrow -->
    <div style="flex-shrink: 0; width: 100px; height: 6px; background-color: #28a799; position: relative;">
      <div style="position: absolute; right: -10; top: 50%; transform: translateY(-50%); border-top: 18px solid transparent; border-bottom: 18px solid transparent; border-left: 24px solid #28a799;"></div>
    </div>
    <!-- Right stacked three boxes -->
    <div style="flex-shrink: 0; display: flex; flex-direction: column; gap: 24px;">
      <div style="background: #dcf3ee; border-radius: 32px; padding: 24px 40px; font-weight: 600; color: #112236;">PCA: components</div>
      <div style="background: #e8f2fb; border-radius: 32px; padding: 24px 40px; font-weight: 600; color: #112236;">FA: hidden factors</div>
      <div style="background: #fff3dd; border-radius: 32px; padding: 24px 40px; font-weight: 600; color: #112236;">LDA: class-discriminating direction</div>
    </div>
  </div>
</div>

<div style="border-radius: 16px; background-color: #dcf3ee; border-left: 6px solid #28a799; overflow: hidden;">
    <p style="margin: 0; padding: 18px 22px; color: #1a2b42;"><b>Key question: can we reduce complexity without losing useful predictive information?</b></p>
</div>

## Learning Outcomes

### By the end of the lecture, you can…

- Distinguish feature selection from feature extraction.
- Explain how PCA, Factor Analysis and LDA differ.
- Interpret PCA explained variance and component loadings.
- Use dimensionality reduction without data leakage.
- Compare model performance before and after reduction.

## Fundamentals

### Dimensionality reduction in one sentence

Represent a dataset with fewer variables while retaining information useful for the task.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="min-width: max-content;">
    <!-- Top dark banner -->
    <div style="background-color: #12283d; border-radius: 20px; padding: 32px 24px; text-align: center; margin-bottom: 16px;">
      <span style="font-size: 32px; font-weight: 700; color: #ffffff;">Original features</span>
      <span style="font-size: 32px; font-weight: 700; color: #ffffff; margin: 0 24px;">→</span>
      <span style="font-size: 32px; font-weight: 700; color: #ffffff;">fewer features or components</span>
    </div>
    <!-- Two bottom cards side by side -->
    <div style="display: flex; gap: 12px;">
      <!-- Why use it -->
      <div style="flex-shrink: 0; width: 48%; min-width: 600px; border: 1px solid #e2e8f0; border-left: 6px solid #28a799; border-radius: 12px; padding: 28px 24px; background: #ffffff;">
        <h2 style="margin:0 0 20px 0; color: #12283d;">Why use it?</h2>
        <p style="color: #4a5568; line-height: 1.6;">Lower computational cost, cleaner visualisations, potentially less noise.</p>
      </div>
      <!-- What is the risk -->
      <div style="flex-shrink: 0; width: 48%; min-width: 600px; border: 1px solid #e2e8f0; border-left: 6px solid #f2b138; border-radius: 12px; padding: 28px 24px; background: #ffffff;">
        <h2 style="margin:0 0 20px 0; color: #12283d;">What is the risk?</h2>
        <p style="color: #4a5568; line-height: 1.6;">Important information can be lost. Accuracy is not guaranteed to increase.</p>
      </div>
    </div>
  </div>
</div>

### Why do many features become difficult

Three reasons to consider reduction.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display: flex; gap: 12px; min-width: max-content;">
    <!-- Overlap -->
    <div style="flex-shrink: 0; width: 350px; border: 1px solid #e2e8f0; border-left: 6px solid #28a799; border-radius: 12px; padding: 28px 24px; background: #ffffff;">
      <h2 style="margin:0 0 20px 0; color: #12283d;">Overlap</h2>
      <p style="color: #4a5568; line-height: 1.6;">Two measurements may capture similar underlying information.</p>
      <p style="color: #4a5568; line-height: 1.6; margin-top:20px;">Example: haemoglobin and haematocrit can be related.</p>
    </div>
    <!-- Noise -->
    <div style="flex-shrink: 0; width: 350px; border: 1px solid #e2e8f0; border-left: 6px solid #346899; border-radius: 12px; padding: 28px 24px; background: #ffffff;">
      <h2 style="margin:0 0 20px 0; color: #12283d;">Noise</h2>
      <p style="color: #4a5568; line-height: 1.6;">Some features may contain variation that does not help predict the outcome.</p>
    </div>
    <!-- Complexity -->
    <div style="flex-shrink: 0; width: 360px; border: 1px solid #e2e8f0; border-left: 6px solid #f2b138; border-radius: 12px; padding: 28px 24px; background: #ffffff;">
      <h2 style="margin:0 0 20px 0; color: #12283d;">Complexity</h2>
      <p style="color: #4a5568; line-height: 1.6;">More dimensions can make distances less informative and some models slower.</p>
    </div>
  </div>
</div>

<div style="border-radius: 16px; background-color: #dcf3ee; border-left: 6px solid #28a799; overflow: hidden;">
    <p style="margin: 0; padding: 18px 22px; color: #1a2b42;"><b>More features ≠ more useful information.</b></p>
</div>

### Correlated features: a visual intuition

Two variables often change together. One combined direction may summarise them.

![](img/Pasted_image_20261117172550.png)

## Connection to week 4

### Feature selection vs feature extraction

The two approaches both reduce dimensions, but they do different things.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display: flex; gap: 24px; min-width: max-content;">
    <!-- Feature Selection -->
    <div style="flex-shrink: 0; width: 500px; border: 1px solid #e2e8f0; border-radius: 20px; padding: 32px; background: #ffffff;">
      <h2 style="margin:0 0 24px 0; color:#28a799;">FEATURE SELECTION</h2>
      <p style="font-size: 20px; color:#4a5568; margin-bottom: 32px;">Keep original columns</p>
      <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; margin-bottom:40px;">
        <span style="background:#edf0f2; border-radius:999px; padding:14px 28px;  color:#4a5568; font-weight:600;">age</span>
        <span style="background:#dcf3ee; border-radius:999px; padding:14px 28px; color:#28a799; font-weight:600;">bp</span>
        <span style="background:#dcf3ee; border-radius:999px; padding:14px 28px; color:#28a799; font-weight:600;">sg</span>
        <span style="background:#dcf3ee; border-radius:999px; padding:14px 28px; color:#28a799; font-weight:600;">hemo</span>
        <span style="background:#edf0f2; border-radius:999px; padding:14px 28px; color:#4a5568; font-weight:600;">sc</span>
        <span style="background:#dcf3ee; border-radius:999px; padding:14px 28px; color:#28a799; font-weight:600;">pcv</span>
      </div>
      <br><br>
      <p style="font-size: 20px; color:#4a5568;">Lasso / Boruta / RFECV</p>
    </div>
    <!-- Feature Extraction -->
    <div style="flex-shrink: 0; width: 500px; border: 1px solid #e2e8f0; border-radius: 20px; padding: 32px; background: #ffffff;">
      <h2 style="margin:0 0 24px 0; color:#346899;">FEATURE EXTRACTION</h2>
      <p style="font-size: 20px; color:#4a5568; margin-bottom: 32px;">Create new variables</p>
      <div style="display: flex; flex-direction: column; gap: 20px; margin-bottom:40px;">
        <span style="background:#e8f2fb; border-radius:999px; padding:14px 28px; color:#346899; font-weight:600;">Component 1</span>
        <span style="background:#e8f2fb; border-radius:999px; padding:14px 28px; color:#346899; font-weight:600;">Component 2</span>
        <span style="background:#e8f2fb; border-radius:999px; padding:14px 28px; color:#346899; font-weight:600;">Component 3</span>
      </div>
      <p style="font-size: 20px; color:#4a5568;">PCA / FA / LDA</p>
    </div>
  </div>
</div>

## Fundamentals

### Three methods, three learning signals

The methods do not optimise the same objective.

| Method          | What it tries to preserve | Target labels | Typical use                |
| --------------- | ------------------------- | ------------- | -------------------------- |
| PCA             | Overall variance          | Not used      | Compression; visualisation |
| Factor Analysis | Shared covariance         | Not used      | Latent structure           |
| LDA             | Class separation          | Required      | Supervised projection      |

## Reliable Experiments

### Avoid data leakage before reducing dimensions

Fit every learned transformation on training data only.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display:flex; align-items:center; gap:16px; min-width:max-content;">
    <!-- Step 1 -->
    <div style="flex-shrink:0; width:420px; background:#e8f2f3; border-radius:24px; padding:40px 20px; text-align:center;">
      <p style="font-size:20px; font-weight:700; color:#1a2b3c; margin:0 0 20px 0;">TRAIN / TEST SPLIT</p>
      <p style="color:#28a799; margin:0;">first</p>
    </div>
    <span style="font-size:48px; color:#28a799; font-weight:bold;">→</span>
    <!-- Step 2 -->
    <div style="flex-shrink:0; width:420px; background:#e8f2f3; border-radius:24px; padding:40px 20px; text-align:center;">
      <p style="font-size:20px; font-weight:700; color:#1a2b3c; margin:0 0 20px 0;">PREPROCESS</p>
      <p style="color:#28a799; margin:0;">fit in train fold</p>
    </div>
    <span style="font-size:48px; color:#28a799; font-weight:bold;">→</span>
    <!-- Step 3 -->
    <div style="flex-shrink:0; width:420px; background:#e8f2f3; border-radius:24px; padding:40px 20px; text-align:center;">
      <p style="font-size:20px; font-weight:700; color:#1a2b3c; margin:0 0 20px 0;">REDUCE</p>
      <p style="color:#28a799; margin:0;">fit in train fold</p>
    </div>
    <span style="font-size:48px; color:#28a799; font-weight:bold;">→</span>
    <!-- Step 4 -->
    <div style="flex-shrink:0; width:420px; background:#e8f2f3; border-radius:24px; padding:40px 20px; text-align:center;">
      <p style="font-size:20px; font-weight:700; color:#1a2b3c; margin:0 0 20px 0;">CLASSIFIER</p>
      <p style="color:#28a799; margin:0;">fit in train fold</p>
    </div>
    <span style="font-size:48px; color:#28a799; font-weight:bold;">→</span>
    <!-- Step 5 (highlight) -->
    <div style="flex-shrink:0; width:420px; background:#dcf3ee; border-radius:24px; padding:40px 20px; text-align:center;">
      <p style="font-size:20px; font-weight:700; color:#1a2b3c; margin:0 0 20px 0;">EVALUATE</p>
      <p style="color:#28a799; margin:0;">test held out</p>
    </div>
  </div>
</div>

<div style="border-radius: 16px; background-color: #dcf3ee; border-left: 6px solid #28a799; overflow: hidden;">
    <p style="margin: 0; padding: 18px 22px; color: #1a2b42;"><b>Use a Pipeline so cross-validation refits preprocessing and reduction inside each training fold.</b></p>
</div>

## Section 01 / Unsupervised

### Principal Component Analysis

Find new directions that capture the largest variation in the dataset.

### Principal Component Analysis (PCA)

PCA is a dimensionality reduction technique that transforms features into a new set of linearly uncorrelated components (called principal components).

How it works:

- PCA identifies the directions (components) along which the variance in the data is maximized. 
- Each principal component is a combination of the original features, capturing the most variance. 

Key Benefits:

- Reduces the dimensionality of large datasets while retaining most of the variance. 
- Makes data easier to visualize and interpret. 

When to use:  
In datasets with many correlated features, to reduce the dataset while retaining the majority of its variance. 

### PCA rotates the view of the data

The first component follows the largest spread; the second is perpendicular.

![](img/Pasted_image_20261117175438.png)

### Principal components are new features

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="min-width: max-content;">
    <!-- 顶部深色公式栏 -->
    <div style="background:#122638; border-radius:24px; padding:40px 32px; margin-bottom:24px;">
      <h2 style="color:#ffffff; margin:0; white-space:nowrap;"><center>PC1 &nbsp;=&nbsp; a<sub>1</sub> × age &nbsp;+&nbsp; a<sub>2</sub> × bp &nbsp;+&nbsp; a<sub>3</sub> × hemo &nbsp;+&nbsp; ...</center></h2>
    </div>
    <!-- 下方三卡片行 -->
    <div style="display:flex; gap:24px;">
      <!-- PC1 -->
      <div style="flex-shrink:0; width:350px; border:1px solid #e2e8f0; border-left:12px solid #28a799; border-radius:20px; padding:32px; background: #ffffff;">
        <h2 style="color:#1a2b3c; margin:0 0 12px 0;">PC1</h2>
        <p style="color:#4a5568; margin:0; line-height:1.4;">Largest possible variance of any linear projection.</p>
      </div>
      <!-- PC2 -->
      <div style="flex-shrink:0; width:350px; border:1px solid #e2e8f0; border-left:12px solid #28a799; border-radius:20px; padding:32px; background: #ffffff;">
        <h2 style="color:#1a2b3c; margin:0 0 12px 0;">PC2</h2>
        <p style="color:#4a5568; margin:0; line-height:1.4;">Next-largest variance; uncorrelated with PC1.</p>
      </div>
      <!-- PC3,PC4... -->
      <div style="flex-shrink:0; width:350px; border:1px solid #e2e8f0; border-left:12px solid #28a799; border-radius:20px; padding:32px; background: #ffffff;">
        <h2 style="color:#1a2b3c; margin:0 0 12px 0;">PC3, PC4, ...</h2>
        <p style="color:#4a5568; margin:0; line-height:1.4;">Additional directions explain progressively smaller variance.</p>
      </div>
    </div>
  </div>
</div>

The coefficients a1, a2 and so on are learned by PCA and called loadings or weights, depending on context. PCA creates new features by combining original features with different weights. PC1 captures the most variation, followed by PC2, PC3, and so on.

### PCA in four simple operations

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display:flex; gap:24px; min-width:max-content;">
    <!-- Step 1 -->
    <div style="flex-shrink:0; width:360px; border:1px solid #e2e8f0; border-radius:20px; padding:32px; background: #ffffff;">
      <span style="display:inline-block; background:#dcf3ee; color:#28a799; font-size:32px; font-weight:700; border-radius:999px; width:72px; height:72px; line-height:72px; text-align:center; margin-bottom:24px;">1</span>
      <h2 style="color:#1a2b3c; margin:0 0 24px 0;">Prepare</h2>
      <p style="color:#4a5568; margin:0; line-height:1.4;">Impute and scale numerical features</p>
    </div>
    <!-- Step 2 -->
    <div style="flex-shrink:0; width:360px; border:1px solid #e2e8f0; border-radius:20px; padding:32px; background: #ffffff;">
      <span style="display:inline-block; background:#dcf3ee; color:#28a799; font-size:32px; font-weight:700; border-radius:999px; width:72px; height:72px; line-height:72px; text-align:center; margin-bottom:24px;">2</span>
      <h2 style="color:#1a2b3c; margin:0 0 24px 0;">Find axes</h2>
      <p style="color:#4a5568; margin:0; line-height:1.4;">Calculate principal directions directions</p>
    </div>
    <!-- Step 3 -->
    <div style="flex-shrink:0; width:360px; border:1px solid #e2e8f0; border-radius:20px; padding:32px; background: #ffffff;">
      <span style="display:inline-block; background:#dcf3ee; color:#28a799; font-size:32px; font-weight:700; border-radius:999px; width:72px; height:72px; line-height:72px; text-align:center; margin-bottom:24px;">3</span>
      <h2 style="color:#1a2b3c; margin:0 0 24px 0;">Rank</h2>
      <p style="color:#4a5568; margin:0; line-height:1.4;">Order by explained variance</p>
    </div>
    <!-- Step 4 -->
    <div style="flex-shrink:0; width:360px; border:1px solid #e2e8f0; border-radius:20px; padding:32px; background: #ffffff;">
      <span style="display:inline-block; background:#dcf3ee; color:#28a799; font-size:32px; font-weight:700; border-radius:999px; width:72px; height:72px; line-height:72px; text-align:center; margin-bottom:24px;">4</span>
      <h2 style="color:#1a2b3c; margin:0 0 24px 0;">Transform</h2>
      <p style="color:#4a5568; margin:0; line-height:1.4;">Project data onto first k components</p>
    </div>
  </div>
</div>

#### Explained variance: what does 95% mean

The selected components retain 95% of variance in the fitted feature representation.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display: flex; align-items: flex-start; gap: 30px; min-width: max-content;">
    <!-- 左侧条形图区域 -->
    <div style="padding-top: 8px;">
      <div style="display: flex; align-items: center; margin-bottom: 10px;">
        <span style="width: 30px; font-size: 15px; font-weight: 700; color: #1a2b3c;">PC1</span>
        <div style="width: 560px; height: 22px; background: #288880; border-radius: 11px; margin: 0 6px;"></div>
        <span style="font-size: 15px; color: #4a5568;">32%</span>
      </div>
      <div style="display: flex; align-items: center; margin-bottom: 10px;">
        <span style="width: 30px; font-size: 15px; font-weight: 700; color: #1a2b3c;">PC2</span>
        <div style="width: 350px; height: 22px; background: #288880; border-radius: 11px; margin: 0 6px;"></div>
        <span style="font-size: 15px; color: #4a5568;">20%</span>
      </div>
      <div style="display: flex; align-items: center; margin-bottom: 10px;">
        <span style="width: 30px; font-size: 15px; font-weight: 700; color: #1a2b3c;">PC3</span>
        <div style="width: 265px; height: 22px; background: #288880; border-radius: 11px; margin: 0 6px;"></div>
        <span style="font-size: 15px; color: #4a5568;">15%</span>
      </div>
      <div style="display: flex; align-items: center; margin-bottom: 10px;">
        <span style="width: 30px; font-size: 15px; font-weight: 700; color: #1a2b3c;">PC4</span>
        <div style="width: 195px; height: 22px; background: #288880; border-radius: 11px; margin: 0 6px;"></div>
        <span style="font-size: 15px; color: #4a5568;">11%</span>
      </div>
      <div style="display: flex; align-items: center; margin-bottom: 10px;">
        <span style="width: 30px; font-size: 15px; font-weight: 700; color: #1a2b3c;">PC5</span>
        <div style="width: 125px; height: 22px; background: #288880; border-radius: 11px; margin: 0 6px;"></div>
        <span style="font-size: 15px; color: #4a5568;">7%</span>
      </div>
      <div style="display: flex; align-items: center; margin-bottom: 10px;">
        <span style="width: 30px; font-size: 15px; font-weight: 700; color: #1a2b3c;">PC6</span>
        <div style="width: 90px; height: 22px; background: #48b8b8; border-radius: 11px; margin: 0 6px;"></div>
        <span style="font-size: 15px; color: #4a5568;">5%</span>
      </div>
      <div style="display: flex; align-items: center; margin-bottom: 10px;">
        <span style="width: 30px; font-size: 15px; font-weight: 700; color: #1a2b3c;">PC7</span>
        <div style="width: 70px; height: 22px; background: #48b8b8; border-radius: 11px; margin: 0 6px;"></div>
        <span style="font-size: 15px; color: #4a5568;">4%</span>
      </div>
      <div style="display: flex; align-items: center; margin-bottom: 10px;">
        <span style="width: 30px; font-size: 15px; font-weight: 700; color: #1a2b3c;">PC8</span>
        <div style="width: 55px; height: 22px; background: #48b8b8; border-radius: 11px; margin: 0 6px;"></div>
        <span style="font-size: 15px; color: #4a5568;">3%</span>
      </div>
      <div style="display: flex; align-items: center;">
        <span style="width: 30px; font-size: 15px; font-weight: 700; color: #1a2b3c;">PC9</span>
        <div style="width: 55px; height: 22px; background: #48b8b8; border-radius: 11px; margin: 0 6px;"></div>
        <span style="font-size: 15px; color: #4a5568;">3%</span>
      </div>
    </div>
    <!-- 右侧深色卡片 -->
    <div style="flex-shrink: 0; background: #122638; border-radius: 12px; padding: 24px 30px; text-align: center;">
      <p style="font-size: 44px; font-weight: 700; color: #ffffff; margin:0 0 8px 0;">95%</p>
      <p style="font-size: 16px; color: #b8e2de; margin:0;">illustrative threshold</p>
    </div>
  </div>
</div>

These bar values are illustrative. The explained variance ratio tells what fraction of total fitted-feature variance each component captures. A 95% threshold selects the smallest number of PCs whose cumulative ratio reaches at least 0.95. This does not mean that the resulting classifier has 95% accuracy, that 95% of diagnoses are preserved, or that the method keeps 95% of causal information.

A lower variance threshold means fewer components and more information loss. A higher threshold preserves more variation but requires more components.

## Section 02 / Unsupervised

### Factor Analysis

Find hidden factors that explain correlations among observed variables.

### Factor Analysis (FA)

Factor Analysis is used to model the covariance structure between features and identify hidden factors that explain this structure.

How it works:

- Features are grouped together into a smaller number of "factors," which represent common trends or patterns.

Key Benefits:

- Reduces the dimensionality of data by focusing on key factors driving correlations between features.
- Identifies underlying structures in the dataset.

When to use:  
When you suspect that some of your features are highly correlated and can be grouped into factors.

### A hidden factor behind several measurements

```mermaid
graph TD
    F1["Latent factor F₁"]
    A["Measurement A"]
    B["Measurement B"]
    C["Measurement C"]

    F1 --> A
    F1 --> B
    F1 --> C

    classDef latent stroke:none
    classDef a fill:#e2f4f0,color:#0f243a,stroke:none
    classDef b fill:#e8f2fb,color:#0f243a,stroke:none
    classDef c fill:#fcf2de,color:#0f243a,stroke:none

    class F1 latent
    class A a
    class B b
    class C c
```

<center>Shared influences  +  feature-specific variation</center>

### The FA model in plain language

Every observed feature contains shared structure and some unique variation.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="min-width: max-content;">
    <!-- 顶部深色标题栏 -->
    <div style="background: #122638; border-radius: 24px; padding: 36px 24px; text-align: center; margin-bottom: 24px;">
      <h2 style="color: #ffffff; margin: 0;">Observed measurements = factor loadings × hidden factors + unique noise</h2>
    </div>
    <!-- 下方三卡片行 -->
    <div style="display: flex; gap: 24px;">
      <!-- Factor scores 左侧绿边 -->
      <div style="flex-shrink: 0; width: 350px; border: 1px solid #e2e8f0; border-left: 10px solid #288880; border-radius: 20px; padding: 32px; background: #ffffff;">
        <h3 style="color: #1a2b3c; margin: 0 0 20px 0;">Factor scores</h3>
        <p style="color: #4a5568; line-height: 1.4; margin: 0;">Estimated hidden-factor values for each patient.</p>
      </div>
      <!-- Factor loadings 中间蓝边 -->
      <div style="flex-shrink: 0; width: 350px; border: 1px solid #e2e8f0; border-left: 10px solid #3470a2; border-radius: 20px; padding: 32px; background: #ffffff;">
        <h3 style="color: #1a2b3c; margin: 0 0 20px 0;">Factor loadings</h3>
        <p style="color: #4a5568; line-height: 1.4; margin: 0;">How strongly each observed feature relates to a factor.</p>
      </div>
      <!-- Uniqueness 右侧黄边 -->
      <div style="flex-shrink: 0; width: 350px; border: 1px solid #e2e8f0; border-left: 10px solid #f2b851; border-radius: 20px; padding: 32px; background: #ffffff;">
        <h3 style="color: #1a2b3c; margin: 0 0 20px 0;">Uniqueness</h3>
        <p style="color: #4a5568; line-height: 1.4; margin: 0;">Feature-specific variation not explained by common factors.</p>
      </div>
    </div>
  </div>
</div>

Factor Analysis looks for hidden factors shared by several features. Factor loadings describe how strongly the features relate to those factors, factor scores estimate their values for each patient, and uniqueness represents what the factors cannot explain.

Factor loadings are learned from the relationships between features. Factor scores are then estimated for each patient using their feature values. We do not manually assign these numbers; Factor Analysis calculates them.

### How many factors should we keep

- Start from the scientific question: how many plausible latent factors?
- Inspect factor loadings and whether they make sense.
- Compare model fit or downstream validation performance.
- Report the chosen number of factors and its justification.

Unlike PCA, where we can choose a 95% explained-variance threshold, FA usually requires us to decide the number of factors by examining their meaning, model fit, or validation performance.

### Reading factor loadings

A factor is meaningful only if its high-loading features form an interpretable pattern.

|Feature|Factor 1|Factor 2|
|---|---|---|
|hemo|0.71|0.09|
|pcv|0.66|0.02|
|rc|0.58|-0.06|
|sc|-0.07|0.63|
|bu|-0.04|0.59|
|bp|0.12|0.16|

Not every feature must be strongly related to a hidden factor. Blood pressure has low loadings on both factors, so neither explains much of its variation.

## Section 03 / Supervised

### Linear Discriminant Analysis

Find a projection that best separates the known classes.

### Linear Discriminant Analysis (LDA)

LDA is a supervised dimensionality reduction technique that finds the linear combinations of features that best separate different classes.

How it works:

- LDA creates new axes (linear combinations of features) that maximize the distance between class means while minimizing variance within classes. 
- It reduces the number of dimensions while maximizing class separability. 

Key Benefits:

- Ideal for classification problems where you want to reduce dimensionality while improving class separation. 

When to use:  
In classification problems with high-dimensional data and when class separability is crucial.

### LDA searches for class separation

Unlike PCA, it uses the CKD / non-CKD labels during training.

![](img/Pasted_image_20261117192907.png)

LDA finds a line where patients from different classes become as separated as possible when we project their data points onto it. Each patient then gets a new numerical value representing their position along that line.

### LDA balances two competing objectives

We want classes to be far apart and each class relatively compact.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display: flex; gap: 24px; min-width: max-content;">
    <!-- 左卡片 绿左边框 -->
    <div style="flex-shrink: 0; width: 450px; border: 1px solid #e2e8f0; border-left:10px solid #288880; border-radius:20px; padding:32px; background: #ffffff;">
      <h2 style="color:#1a2b3c; margin:0 0 20px 0;">Increase between-class separation</h2>
      <p style="color:#4a5568; line-height:1.4; margin:0;">Make the projected CKD and non-CKD group centres more distinct.</p>
    </div>
    <!-- 右卡片 蓝左边框 -->
    <div style="flex-shrink: 0; width: 450px; border: 1px solid #e2e8f0; border-left:10px solid #3470a2; border-radius:20px; padding:32px; background: #ffffff;">
      <h2 style="color:#1a2b3c; margin:0 0 20px 0;">Reduce within-class spread</h2>
      <p style="color:#4a5568; line-height:1.4; margin:0;">Avoid a projection where each group spreads widely and overlaps.</p>
    </div>
  </div>
</div>

LDA tries to find a direction where patients from different classes are far apart, while patients from the same class stay close together. This makes the classes easier to distinguish.

Important: LDA does not physically move patients closer together. It selects a projection direction that maximizes the separation between class centres relative to the variation within each class.

### Critical rule: two classes mean one LDA component

Maximum transformed dimensions = number of classes − 1.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="min-width: max-content;">
    <!-- 顶部深色标题栏 -->
    <div style="background: #122638; border-radius: 24px; padding: 36px 24px; text-align: center; margin-bottom: 24px;">
      <h2 style="color: #ffffff; margin: 0;">2 classes − 1 = 1 discriminant component</h2>
    </div>
    <!-- 下方两卡片行 -->
    <div style="display: flex; gap: 24px;">
      <!-- CKD dataset 绿左边框 -->
      <div style="flex-shrink: 0; width: 450px; border: 1px solid #e2e8f0; border-left:10px solid #288880; border-radius:20px; padding:32px; background: #ffffff;">
        <h3 style="color:#1a2b3c; margin:0 0 20px 0;">CKD dataset</h3>
        <p style="color:#4a5568; line-height:1.4; margin:0;">CKD / non-CKD → at most 1 LDA component.</p>
      </div>
      <!-- Three-class example 蓝左边框 -->
      <div style="flex-shrink: 0; width: 450px; border: 1px solid #e2e8f0; border-left:10px solid #3470a2; border-radius:20px; padding:32px; background: #ffffff;">
        <h3 style="color:#1a2b3c; margin:0 0 20px 0;">Three-class example</h3>
        <p style="color:#4a5568; line-height:1.4; margin:0;">3 classes → at most 2 LDA components.</p>
      </div>
    </div>
  </div>
</div>

### PCA vs LDA: what is the key difference? <mark>for CKD dataset</mark>

|Aspect|PCA|LDA|
|---|---|---|
|Learning type|Unsupervised|Supervised|
|Uses y labels?|No|Yes|
|Best direction|Highest variance|Best class separation|
|For binary CKD|Several PCs possible|At most 1 LD|
|Main risk|Discard class signal|Overfit / assumptions|

### Why LDA must stay inside cross-validation

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display: flex; gap: 32px; min-width: max-content;">
    <!-- 左侧 INCORRECT 浅红卡片 -->
    <div style="flex-shrink: 0; width: 400px; background-color: #fce8e8; border-radius: 24px; padding: 40px;">
      <h2 style="color: #b84444; margin: 0 0 36px 0;">INCORRECT</h2>
      <p style="color: #1a2b3c; line-height: 1.4; margin: 0;">Fit LDA on the full dataset, then split or cross-validate.</p>
    </div>
    <!-- 右侧 CORRECT 浅绿卡片 -->
    <div style="flex-shrink: 0; width: 400px; background-color: #dcf3f0; border-radius: 24px; padding: 40px;">
      <h2 style="color: #188074; margin: 0 0 36px 0;">CORRECT</h2>
      <p style="color: #1a2b3c; line-height: 1.4; margin: 0;">Put LDA inside the Pipeline; fit it within each training fold.</p>
    </div>
  </div>
</div>

<div style="border-radius: 16px; background-color: #dcf3ee; border-left: 6px solid #28a799; overflow: hidden;">
    <p style="margin: 0; padding: 18px 22px; color: #1a2b42;"><b>The test labels should never influence feature extraction.</b></p>
</div>

## Putting It Together

### One-page comparison

A compact reference slide for the three techniques.

|                    | PCA                  | FA                | LDA                    |
| ------------------ | -------------------- | ----------------- | ---------------------- |
| Supervision        | Unsupervised         | Unsupervised      | Supervised             |
| What is learned    | Principal directions | Latent factors    | Discriminant axes      |
| Optimises / models | Total variance       | Shared covariance | Class separation       |
| Binary CKD limit   | Up to features       | Up to features    | 1 dimension            |
| Good starting use  | Compression          | Latent structure  | Class-based projection |

## Evaluation

### Compare against the all-features baseline

Keep everything constant except the dimensionality-reduction method.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display: grid; grid-template-columns: 300px 300px; gap: 24px; min-width: max-content;">
    <!-- 左上深色卡片 -->
    <div style="background-color: #122638; border-radius: 20px; padding: 32px;">
      <h2 style="color:#ffffff; margin:0 0 20px 0;">All features</h2>
      <p style="color:#b2e0e0; line-height:1.4; margin:0;">No reduction</p>
    </div>
    <!-- 右上白色卡片 -->
    <div style="border:1px solid #e2e8f0; border-radius:20px; padding:32px; background: #ffffff;">
      <h2 style="color:#1a2b3c; margin:0 0 20px 0;">PCA</h2>
      <p style="color:#4a5568; line-height:1.4; margin:0;">95% variance</p>
    </div>
    <!-- 左下白色卡片 -->
    <div style="border:1px solid #e2e8f0; border-radius:20px; padding:32px; background: #ffffff;">
      <h2 style="color:#1a2b3c; margin:0 0 20px 0;">FA</h2>
      <p style="color:#4a5568; line-height:1.4; margin:0;">5 factors (illustrative)</p>
    </div>
    <!-- 右下白色卡片 -->
    <div style="border:1px solid #e2e8f0; border-radius:20px; padding:32px; background: #ffffff;">
      <h2 style="color:#1a2b3c; margin:0 0 20px 0;">LDA</h2>
      <p style="color:#4a5568; line-height:1.4; margin:0;">1 direction (binary)</p>
    </div>
  </div>
</div>

### What should the comparison report

Accuracy alone is not enough for a clinical classification example.

|Metric|Question it answers|
|---|---|
|Validation accuracy|Does performance hold across training folds?|
|Test accuracy|How many unseen test patients were correct?|
|CKD recall|How many true CKD cases were detected?|
|Specificity|How many non-CKD patients were identified?|
|F1 / ROC-AUC|How does discrimination behave overall?|
|Training time|Did reduction reduce computational cost?|

## Critical Thinking

### When dimensionality reduction hurts

Not every reduction is a success.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="display: flex; gap: 24px;">
    <!-- 左侧 Lost signal，红左边框 -->
    <div style="flex: 0 0 400px; border: 1px solid #e2e8f0; border-left: 8px solid #c84242; border-radius: 16px; padding: 28px; background: #ffffff;">
      <h2 style="color:#1a2b3c; margin:0 0 20px 0;">Lost signal</h2>
      <p style="color:#4a5568; line-height:1.5; margin:0 0 24px 0;">A removed direction may contain disease-related information.</p>
      <p style="color:#4a5568; line-height:1.5; margin:0;">CKD example: PCA might discard a direction containing useful information for identifying kidney disease because it explains only a small amount of variance.</p>
    </div>
    <!-- 中间 Model mismatch，橙左边框 -->
    <div style="flex: 0 0 400px; border: 1px solid #e2e8f0; border-left: 8px solid #f2b040; border-radius: 16px; padding: 28px; background: #ffffff;">
      <h2 style="color:#1a2b3c; margin:0 0 20px 0;">Model mismatch</h2>
      <p style="color:#4a5568; line-height:1.5; margin:0 0 24px 0;">FA assumptions or PCA’s variance objective may not suit a dataset.</p>
      <p style="color:#4a5568; line-height:1.5; margin:0;">CKD example: Factor Analysis (FA) assumes that hidden factors explain relationships between features. If those assumptions do not fit our data, the extracted factors may not be useful.</p>
    </div>
    <!-- 右侧 Too few components，蓝左边框 -->
    <div style="flex: 0 0 400px; border: 1px solid #e2e8f0; border-left: 8px solid #2b689c; border-radius: 16px; padding: 28px; background: #ffffff;">
      <h2 style="color:#1a2b3c; margin:0 0 20px 0;">Too few components</h2>
      <p style="color:#4a5568; line-height:1.5; margin:0 0 24px 0;">An aggressively small representation can underfit.</p>
      <p style="color:#4a5568; line-height:1.5; margin:0;">CKD example: Reducing 24 features to just 1 component might remove important information, making it difficult for the classifier to distinguish CKD from non-CKD patients.</p>
    </div>
  </div>
</div>

Dimensionality reduction is not always beneficial. If we remove useful information, choose an unsuitable method, or keep too few components, our model's performance may decrease. That is why we should compare classification performance before and after dimensionality reduction.

## Takeaways

### Five points to remember

The method matters, but experimental design matters more.

- Feature selection keeps columns; feature extraction makes new ones.
- PCA captures variance.
- Factor Analysis models shared latent structure.
- LDA uses class labels to maximise separation.
- Fit reduction inside cross-validation and compare a baseline.

<div style="overflow-x: auto; padding: 8px 0;">
  <div style="background: #122638; border-radius: 24px; padding: 24px 32px; text-align: center; white-space: nowrap; min-width: max-content;">
    <p style="font-weight: 700; color: #ffffff; margin: 0;">Next: implement PCA / FA / LDA and explain what the results actually mean.</p>
  </div>
</div>

Source: [week7dimensionalityreductionlecture.pptx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fweek7dimensionalityreductionlecture.pptx&wdOrigin=BROWSELINK)
