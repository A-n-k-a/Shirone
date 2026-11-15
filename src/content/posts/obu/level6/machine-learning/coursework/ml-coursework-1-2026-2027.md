---
title: "CHC6089 Machine Learning Coursework 1: Comparative Evaluation of Optimised Machine Learning Models Using Feature Selection and Hyperparameter Tuning"
published: 2026-11-06
publishedAt: 2026-11-06T01:38:00+08:00
description: "For this coursework 1, you are required to design, implement, evaluate, and compare different supervised machine learning models using the UCI Machine Learning Repository dataset individually assigned to you by the module leader."
image: "./151834948.jpg"
tags: ["Coursework"]
category: "Machine Learning"
draft: false
pinned: false
lang: en
---

<center><h4>OXFORD BROOKES UNIVERSITY - CDUT</h4><h4>OBU COMPUTING</h4><h4>Module: CHC6089 Machine Learning (Semester 1, 2026/27)</h4><h5>Coursework 1 Title: Comparative Evaluation of Optimised Machine Learning Models Using Feature Selection and Hyperparameter Tuning</h5></center>

For this coursework 1, you are required to design, implement, evaluate, and compare different supervised machine learning models using the UCI Machine Learning Repository dataset individually assigned to you by the module leader. The practical work must be carried out using Python and appropriate machine learning libraries. The coursework requires you to investigate the effect of different feature-selection approaches on machine learning performance. You must implement and optimise three feature-selection techniques, selected from the methods covered in the module, specifically **Boruta, LASSO, and Recursive Feature Elimination (RFE)**. The selected feature sets must subsequently be used with the required machine learning models to investigate and compare their performance. In addition, you are required to perform hyperparameter optimisation using **Scikit-learn's GridSearchCV** for each of the eight specified machine learning approaches. **You must not simply train the models using their default Scikit-learn configurations.** Instead, an appropriate grid of hyperparameter values should be established and evaluated through grid search to identify a suitable optimised configuration for each model. Your selection of parameters and configuration of the grid search should be justified using the concepts and techniques introduced during the module seminars. You should make appropriate use of the seminar presentations, demonstrations, and programming materials provided during the module. Your work should cover the main stages of the machine learning process, including dataset collection, data preprocessing, data visualisation, handling missing data and data imbalance, data normalisation, optimisation of the three selected feature-selection techniques, grid search configuration for the eight machine learning models, training and testing of the optimised models, and evaluation of their performance. You are expected to discuss and compare your findings and provide a reasonable conclusion based on your results. The main aim of this coursework is to assess your ability to apply the theoretical concepts covered in the module to a real-world machine learning problem and to critically analyse the performance and findings of different approaches. **Each student is expected to use only their individual dataset assigned by the module leader.** Using a different dataset will result in a 20% penalty to discourage academic dishonesty. This coursework 1 is worth 30% of the module mark. **Note that the eight machine learning models include the model already explained in class hours and they include support vector machine (SVM), logistic regression (LR), K-nearest neighbour (KNN), Decision tree (DT), adaptive boosting (ADA) , bagging, stacking, and voting classifiers.**

**Learning Outcomes**

1. Evaluate and articulate the issues and challenges in machine learning, including feature selection, model selection, and decision making process for real-life application.
2. Demonstrate a working knowledge of the variety of mathematical techniques normally adopted for machine learning problems, and of their application to creating effective solutions.
3. Critically evaluate the performance, limitations and future findings of a proposed solution to a machine learning problem.
4. Create solutions to machine learning problems using appropriate tools.

**Note:**  
- Review the Entire Coursework 1 Sheet: Carefully read through all the details provided in this coursework 1 specification.
- Referencing: Ensure that all sources are accurately cited using the IEEE referencing style. For guidance, consult the following links: IEEE Referencing.
- Individual Work: This coursework is an individual assignment. University policies regarding plagiarism, collusion, syndication, and cheating are strictly enforced.
- Implementation Tools: Students are permitted to use only ML libraries and jupyter notebook as the IDE for implementing this coursework 1. This restriction aims to prevent outsourcing or purchasing of source code.

You must adhere to the concepts and tools discussed and used during class hours.

**Report Writing Structure (Total 30%)**  
Follow the provided report template, ensuring your report is well-organized and includes the following sections:  

**Abstract (maximum of 250 words): (1%)**  
Summarize the key aspects of your coursework, including the problem, the feature selection methods, models used, the dataset, and the main findings.  

**1.0 Introduction and Literature Review (3%)**  
Introduce the problem of feature selection in supervised learning especially for your given dataset, its importance, and the coursework objectives. Discuss previous works related to feature selection and supervised learning models with focus on your given dataset, highlighting their contributions and limitations.  

**2.0 Methodology (11%)**  
Detail the dataset, preprocessing steps, optimized feature selection techniques, ML models, and hyperparameter tuning and the model architecture. Provide visualizations of the model architecture and design pipeline.  

2.1 Data Collection and Data Preprocessing **(2%)**  
- Explain the data collected from the UCI ML Repository dataset and ensure it is well-structured, with diverse and consistent entries. Also, present the data visualization to discuss the data distribution using any plots like scatter plot, violin plot, ridge plot, kernel distribution plot, boxen plot etc
- Perform and explain the essential preprocessing tasks, including handling missing data, normalizing features, and addressing class imbalances to prepare the dataset for model training and testing.

2.2 Optimize Three Feature Selections **(3%)**  
Implement the three optimize feature selection techniques - Boruta, Recursive Feature elimination (RFE), and Least Absolute Shrinkage and Selection Operator (LASSO). Document the process of selecting relevant features and the mathematical formulas of each of the optimized feature selections that contribute to model performance.  

2.3 GridSearchCV of 8 Optimize ML Model Selection and Optimization **(4%)**  
Select 8 different supervised machine learning models. For each model, apply scikit learn gridsearchCV to enhance its performance. You must document the rationale behind the selection of models and the optimizing process.  

2.4 Data Partitioning and Environment Setup **(1%)**  
Divide the dataset into training, and testing sets with appropriate split ratios based on the dataset size. Also explain the environment setup.  

2.5 Explain and provide visualizations of the model architecture and design pipeline. **(1%)**  

**3.0 Results and Discussion (9% marks)**  
- Train each of the models using the selected features from the optimized feature selection techniques. Also, train with all the entire dataset (without any feature selection). Monitor and document the training progress.
- Test the trained models on the testing set. Evaluate their performance results using various metrics, such as accuracy, sensitivity, specificity, precision, f1-score, ROC-AUC, confusion matrix and time. Discuss the impact of feature selection on model performance and also when there is no feature selection applied. In your report, tabulate the evaluation metrics like accuracy, sensitivity, specificity, precision, f1-score, ROC-AUC and time for all the optimized feature selections and even with no feature selection with all the ML models.
- Present and analyse the experimental results, using tables, figures, and plots. Discuss the effectiveness of the optimized feature selection techniques and their impact on model performance.
- Also, document the learning curves, the confusion matrices and ROC-AUCs of the best ML model with the best optimised feature selections

**4.0 Conclusion, Limitations, and Future Work (3%)**  
Summarize your findings, discuss any limitations encountered, and suggest areas for future work or improvements.  

**5.0 References (1.5%)**  
Cite all sources used, adhering to IEEE citation standards. Include a minimum of 10 relevant references. The three main parts of a reference are as follows:  
1. Author’s name listed as first initial of first name, then full last.
2. Title of article, patent, conference paper, etc., in quotation marks.
3. Title of journal or book in italics

Each reference number should be enclosed in square brackets on the same line as the text, before any punctuation, with a space before the bracket.  
Examples of in-text citation:  
“. . .end of the line for my report \[1\].”  
“The theory was first put forward in 1987 \[2\].”  
“Scholtz \[3\] has argued. . . .” “For example, see \[4\].”  
“Several recent studies \[3, 4, 15, 22\] have suggested that. . . .”  
Reference  
\[1\] S. Bhanndahar. ECE 4321. Class Lecture, Topic: “Bluetooth can’t help you.” School of Electrical and Computer Engineering, Georgia Institute of Technology, Atlanta, GA, Jan. 9, 2008.  

**Technical Writing (1.5%)**  
Adherence to the provided report template, clarity and coherence in writing, and proper formatting of figures, tables, and diagrams. The quality of plots (600dpi) and readability of labels (font size 20-25pt) will also be evaluated. Effectively communicating of ideas and demonstrating critical thinking showing a solid grasp of the subject matter.  

**Assignment Length**  
The length of the assignment should not be less than 2,500 words for the coursework to contribute towards the development of writing skills and critical thinking. Therefore, it is required of you to complete your assignments within the coursework specification as written in the assignment brief. The specified word counts refer to the main body of the report and also include headings, and in-text citations. However, kindly note that the word count does not include front cover, title page, contents page, abstract, tables, reference list, bibliography, appendices, equations or diagrams. Remember to save all images in a specific folder with high image resolution of 600dpi. Also, all tables and Figures images must be well labelled in your report.  

**Font style: Times New Roman, Font Size: 11, Line spacing: 1.0**  
Appendices themselves will not be marked. However, inappropriate use of appendices will be taken into consideration when awarding the final mark.  

**Submission Guidelines:**  
- Report Submission: Submit your report using the single-column ML coursework 1 template provided. Include detailed descriptions of your tasks and results, ensuring clarity and organization. The final submission deadline is Week 8, November 27, 2026 by 17:00. Late submissions will incur a penalty of up to 20 marks. Failure to submit will result in a zero mark. If you face exceptional circumstances, contact the Award Administrator and Module Leader in advance.

File Submission Format: Submit your work in a compressed .zip or .rar file containing:  
- Report: A Microsoft Word document named using the format: `2023xxxxxx_CHC6089_MLCoursework1_Report.docx`
- Experimental Files: A .zip file containing the code, graphs, model architecture, results, and diagrams. Plots/figures/images/diagrams should be saved as 600dpi, and text labels should be 20-25pt.
- Filename: `2023xxxxxx_CHC6089_ MLCoursework1_Files.zip`

**Note: Student MUST submit these three files: the report, all images with 600 dpi each in a folder and the corresponding source code for a complete justification of the ML coursework 1 requirement.**  

**Grading Criteria:**  
- Implementation Accuracy: Proper execution and documentation of all required steps, including data preprocessing, model architecture, and evaluation.
- Metric Calculation: Accurate computation and clear presentation of all the necessary evaluation metrics mentioned in instruction 3.
- Report Quality: Coherent, structured, and well-referenced report writing.
- Critical Analysis: Insightful interpretation of results and discussions on the implications of your findings.
- Presentation: High-quality, legible plots and diagrams.

Note: Start your coursework early to manage the workload effectively. If you need assistance, seek help from your module leader.

Best of luck with your coursework 1!

(AI declaration template can be found in source)

Source: 
- [ml-coursework-12026-2027.pdf](https://vle.zycdut.net/sites/student.zy.cdut.edu.cn/files/attachments/ml-coursework-12026-2027.pdf)
- [l6-2026-2027.xlsx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fl6-2026-2027.xlsx&wdOrigin=BROWSELINK)
