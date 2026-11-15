---
title: "Lecture 6: Test Report and Test Evaluation"
published: 2026-11-10
publishedAt: 2026-11-10T14:30:00+08:00
description: "Review: Software testing techniques; Principles and theories of software testing."
image: "./132064059.png"
tags: ["Software Defects", "Functionality Issues", "Software Inconvenience", "Insufficient Functionality", "Poor Interaction"]
category: "Software Analysis and Testing"
draft: false
pinned: false
lang: en
---

## Review

- Software testing techniques
    - Insert faults into program and perform error-seeding testing
    - Apply mutation operators to model faulty programs and perform mutation analysis
    - Partitioning input space according to specification or implementation
    - Applying domain analysis techniques
- Principles and theories of software testing
    - Subsumption relation between mutation testing and structural testing
    - Error detection ability of domain analysis methods

## Software defects

A software defect is any undesired or unacceptable deviation existing within software (documents, data, programs) that leads to quality issues in the software.

The software defects come in various forms, primarily including malfunctioning features, inconvenience in software usage, inadequate functionalities, poor interaction with software operators, subpar performance, boundary errors, and errors within the software documentation.

## Functionality issues

Functionality issues: The provided functions do not comply with the functionalities specified in the design specification document, or they are simply unusable. This error often occurs in the early and middle stages of the testing process, where many of the functions specified in the design specification document cannot run or produce results that fail to meet the expected outcome.  
The most obvious example is when options and actions provided in the user interface yield no response after user interaction.

## Software inconvenience

Software inconvenience in usage: Whenever software is challenging to use or users are unsure how to utilize it, there must be design issues. User-friendly software is designed to be as convenient as possible, making it easy for users to operate.

## Insufficient functionality

Insufficient functionality provided: This issue is different from malfunctioning functions. Here, it refers to the software's provided functions operating normally but being incomplete for the user. The functionalities of the software operate as per the requirements of the design specifications, yet they are perceived as incomplete from the user's perspective. When evaluating test results, system testers must consider the user's viewpoint in their assessment.

## Poor interaction

Poor interaction with software operators: A good software system must interact seamlessly with its operators. During the use of the software by operators, it is crucial for the software to respond effectively to the operator's actions. For instance, when browsing a website, if an operator enters insufficient or erroneous information on a webpage and attempts to proceed, if the page displays an error message without specifying where the mistake occurred, the operator is left with the only options of returning to the previous page to re-enter the information or abandoning the process.

## The lifecycle of software defects

Discovery to Open: Testing personnel identify a software defect and then report it to the development team.  
Repair: Developers rectify the defect and then submit it to testing personnel for verification.  
Closure: Testing personnel verify the software after the repair, officially closing the defect as it no longer exists.  

## Software Defect Report

Directory
1. Software Defect Report Identifier
2. Summary of Software Defects
3. Description of Software Defects

① Input  
② Expected result  
③ Actual result  
④ Anomalies  
⑤ Date and time  
⑥ Steps when the software defect occurred  
⑦ Testing environment  
⑧ Reproduction testing  
⑨ Testers  
⑩ Witnesses  

4 Impact  

---

1. Software Defect Report Identifier: A unique ID designated for a software defect report, used for locating and referencing purposes.
2. Summary of Software Defects: Concisely state the facts and summarize the software defects. Provide information about the version of the tested software, relevant test cases, and testing instructions. For any confirmed software defects, include related test cases. If a software defect was discovered incidentally, a test case to reproduce this unexpected defect should also be written.

---

Software Defect Description: The individual compiling the software defect report should provide sufficient information in the report for the repair personnel to understand and replicate the sequence of events. The following are the components within a software defect description:  
①Input: Description of the actual inputs used during the testing (e.g., files, keystrokes, etc.).  
②Expected Result: This result stems from the designed outcome of the running test case when the event occurs.  
③Actual Result: Record the actual outcome obtained from the test case during execution.  
④Anomaly: Refers to the extent of the difference between the actual and expected results. It also includes any other data, such as cases involving excessively small or large amounts of system data.  
⑤Date and Time: The date and time when the software defect occurred.  
⑥Steps: The sequence of actions or steps that led to the occurrence of the software defect. This is particularly crucial if a long or complex testing procedure was used.  
⑦Testing Environment: The environment in which the testing was conducted. For instance: system testing environment, acceptance testing environment, client's testing environment, testing location, etc.  
⑧Reproduction Testing: The number of attempts made to replicate or reproduce the test scenario for this specific testing.  
⑨Testers: Information about the personnel who conducted this particular test.  
⑩Witnesses: Details about other individuals who are aware of or witnessed this test.  

4 Impact: The impact in a software defect report indicates the potential consequences of the software defect on users. When reporting a software defect, testing personnel categorize the defect and outline its impact. A commonly used method is to classify software defects based on severity and priority.

## Software testing evaluation

Why do we need to conduct an evaluation of software testing?

Software testing evaluation is conducted for two primary reasons:
1. Quantifying the Testing Process: This aims to assess the state of the software testing process, determining when the software testing can be concluded or is in a state of completion.
2. Generating Quantitative Data for Final Testing or Software Quality Analysis Reports: It provides the quantitative data necessary for generating final testing or software quality analysis reports, such as defect removal efficiency, test coverage, and other related metrics.

## Code-based testing coverage

Code-based testing coverage refers to how much of the code has been exercised during the testing process.  
Code coverage can be established based on control flow (statements, branches, or paths) or data flow. The aim of control flow coverage is to test lines of code, branch conditions, paths within the code, and so on.  
Data flow coverage aims to validate the data state by testing its status through software operations. For example, ensuring that data elements are defined before their use.  

$$\text{Code-based testing coverage} = \frac{\text{Executed lines of code}}{\text{Total lines of code}}
$$

<video controls>
  <source src="https://vle.zycdut.net/sites/student.zy.cdut.edu.cn/files/attachments/software-testing-tutorials-beginners.mp4" type="video/mp4" />
  <p>
    你的浏览器不支持 HTML5 视频。这里有一个<a
      href="https://vle.zycdut.net/sites/student.zy.cdut.edu.cn/files/attachments/software-testing-tutorials-beginners.mp4"
      download="software-testing-tutorials-beginners.mp4"
      >视频</a
    >链接。
  </p>
</video>

Source: [chc6072-lecture6.pptx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fchc6072-lecture6_2.pptx&wdOrigin=BROWSELINK)
