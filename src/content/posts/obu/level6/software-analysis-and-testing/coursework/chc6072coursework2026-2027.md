---
title: "CHC6072: Software Analysis and Testing (Semester 1, 2026-2027) Coursework Specification"
published: 2026-09-29
publishedAt: 2026-09-29T14:30:00+08:00
description: "Analysis and Testing of a Web Application"
image: "./149207271.png"
tags: ["Coursework", "Specification"]
category: "Software Analysis and Testing"
draft: false
pinned: false
lang: en
---

<center><h2>CHC6072: Software Analysis and Testing</h2></center>  
<center>(Semester 1, 2026-2027)</center>  
<center><h1>Coursework Specification</h1></center>  
<center><h2>Analysis and Testing of a Web Application</h2></center>  

---

### 1. Assessed Learning Outcomes

This coursework counts for 70% of the total assessment of this module. It is designed to develop and assess your attainment of the following learning outcomes.

<table>
  <tbody>
    <tr>
      <td>1</td>
      <td>Create effective software test plans to demonstrate an understanding of the principles and theoretical foundations of software quality assurance processes and systems, and software quality assurance methodologies, models and techniques</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Evaluate the strengths and weaknesses of different approaches, based on the theoretical foundations of software measurement and metrics and select and apply appropriate metrics in the context of software creation</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Understand the theoretical foundations of software testing, both static and dynamic, manual and automated;<br>understand the range of applicability of different approaches and techniques, and select and apply appropriate techniques in practical situations</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Design and conduct systematic experiments, using both quantitative and qualitative methods; collect data from the experiments systematically and analyze the results</td>
    </tr>
  </tbody>
</table>

### 2. The problem to be solved

In this coursework, you are required to work individually as a software quality assurance and testing engineer to perform testing and analysis of a given web-based application, and to develop test suites for automated regression testing of the application

The application is the website of the University of Bristol, accessible at https://www.bristol.ac.uk. The specific function of this web-based application to be tested is the online facility for finding undergraduate courses offered by the university. We will focus on one of the following courses: Computer Science, Economics and Accounting, or Marketing

**Note**: _The URL given is an external application beyond the lecturer's control; you must be prepared for possible changes to the website when you write your automated test scripts._

### 3. Tasks to do

The following is a brief description of the tasks and the marking scheme (in terms of the distribution of their weights in the assessment). **A detailed marking scheme** is given in a separate file, also available on the student’s website.

#### Task 1: Developing a test plan (25%)

In this task, you are required to:

- Explore the website to be tested;
- Construct a hyperlink graph model of the application;
- Write a user story or a set of user stories in JBehave format based on the hyperlink graph model of the system. Each user story should include:
    1. a narrative description of the user story
    2. a set of scenarios of using the function

Note that your test plan should achieve node coverage and hyperlink coverage of the hyperlink graph model.

#### Task 2: Developing automated test scripts (25%)

In this task, you are required to follow the steps below to develop a set of automated test scripts based on the result of Task 1.

1. Select a subset of user stories/scenarios (**at least three**) in your test plan as the test cases of your choice.
2. For each scenario of your choice, follow the scenario description to perform a manual test of the web application and record your manual testing process using **Selenium IDE,** which you are required to install on your computer by yourself.
3. Edit and revise the recorded test process of your manual tests to make automated test scripts that are suitable for future regression testing.
4. Group the test scripts for one user story into a test suite.

Note that your chosen test cases should be the most complicated and important ones. Please read the detailed marking scheme for the quality standard that your test cases should have.

#### Task 3: Performing automated testing (30%)

In this task, you are required to perform the following.

1. Execute the test scripts using **Selenium IDE** to test the application in the **web browser** and record test executions in a log file.
2. Translate your test scripts in Selenese into one **Java JUnit Test Code** and execute the Java Test Code using JUnit with your software to test the web application in the **web browser**. You are required to install Selenium WebDriver for Chrome and take screen snapshots to demonstrate the successful executions of test code.

#### Task 4: Measuring test adequacy (20%)

In this task, you are required to calculate the adequacy of your testing by measuring your test’s **node coverage** and **hyperlink coverage** of the hyperlink graph that you developed in Task 1.

### 4. Submission of Coursework

#### 4.1. When to submit

The submission deadline is at **8:00am on Monday of Week 9**.

#### 4.2. What to be submitted

Each student must submit a compressed (zip) file that contains a set of files for the coursework. The file names and their contents to be included in coursework submission must follow the convention given in the table below. The text in red font below should be replaced by the student's own id number.

| **File name**                                          | **Format** | **Example**                                                | **The content**                                                                                         |
| ------------------------------------------------------ | ---------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| CHC6072\_CW\_<span style="color: red">StdID</span>.zip | Zip file   | CHC6072\_CW\_<span style="color: red">156789023</span>.zip | The zip file should contain all the files of the coursework submission. StdID is the student ID number. |
| UserStory.docx                                         | MS Word    | UserStory.docx                                             | The user story and scenario in JBehave format.                                                          |
| TestSuite.side                                         | SIDE       | TestSuite.side                                             | The test suite saved into one Selenium test suite file.                                                 |
| TestCaseName.side                                      | SIDE       | FindUGCourse.side                                          | The test scripts. One file per test case. You<br><br>may need multiple test script files.               |
| Testcase_screenshot.docx                               | MS Word    | Testcase_screenshot.docx                                   | Screenshot of your different test script, and save into word file                                       |
| LogFile.xlsx                                           | Text       | LogFile.txt                                                | The log file of all the test executions in Selenium IDE. One file per student.                          |
| TestClassName.java                                     | Java code  | FindPGCourse.java                                          | The test code in java for JUnit testing with WebDriver. One file for each Junit class.                  |
| TestResult.jpeg                                        | Jpeg       | TestResult.jpg                                             | The screen snapshots of executing Junit and your Java Code                                              |
| LinkGraphAdequacy.docx                                 | MS Word    | Adequacy.docx                                              | The hyperlink graph and your calculation of test adequacy.                                              |

Source: [chc6072coursework2026-2027.docx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fchc6072coursework2026-2027.docx&wdOrigin=BROWSELINK)
