---
title: "CHC6173: Software Engineering (Semester 1, 2026-2027) Coursework Specification"
published: 2026-09-27
description: "Software Engineering of a Modern Computer Application"
image: "./147038120.jpg"
tags: ["Coursework", "Specification"]
category: "Software Engineering"
draft: false
pinned: false
lang: en
---

<center><h5>School of Engineering, Computing and Mathematics<br>
Oxford Brookes University<br>
CHC6173: Software Engineering<br>
(Semester 1, 2026-2027)</h5></center>  
<center><h2>Coursework Specification</h2></center>  
<center><h2>Software Engineering of a Modern Computer Application</h2></center>  

## 1. Assessed Learning Outcomes

This coursework counts as **100%** of the total assessment of this module. It is designed to assess your attainment of the following learning outcomes.

<table>
    <tr>
        <td>1</td>
        <td>Demonstrate an understanding of the software lifecycle and be able to critically analyse a problem to decide on a relevant process model.</td>
    </tr>
    <tr>
        <td>2</td>
        <td>Demonstrate an understanding of the role of risk in a project and be able to identify and manage both risk and the impact of change on a project.</td>
    </tr>
    <tr>
        <td>3</td>
        <td>Demonstrate an understanding of the role of requirements analysis and elicitation and the relationship between requirements and design, and use this knowledge to be able to create functional and non-functional requirements for a project.</td>
    </tr>
    <tr>
        <td>4</td>
        <td>Be able to critically evaluate and utilise design paradigms of object-oriented analysis and design, component-based design, and service-oriented design.</td>
    </tr>
    <tr>
        <td>5</td>
        <td>Describe and employ software techniques in the implementation of designs to achieve desired software quality, including reliability, efficiency and robustness.</td>
    </tr>
    <tr>
        <td>6</td>
        <td>Understand and be able to apply a range of testing methods and techniques. </td>
    </tr>
    <tr>
        <td>7</td>
        <td>Use refactoring in the process of modifying a software component.</td>
    </tr>
    <tr>
        <td>8</td>
        <td>Understand how software reliability contributes to system reliability and be able to apply multiple methods to develop reliability estimates for a software system.</td>
    </tr>
</table>

## 2. The problem to be solved

In this coursework, you are required to work **in a group of 4 students** as a software engineering team to develop[+develop] a given modern computer application by applying appropriate software engineering methodology and technologies. Each member of the team will conduct software engineering activities for developing one subsystem and collaborate with the other members of the team to ensure that these subsystems are integrated and interact with each other to form a consistent system. A brief description of the specific application is given in the document CHC6173-CW-Case Study - v1.0, which is available on the student website.

[+develop]: No coding is required in this coursework.

You are required to perform a series of software engineering tasks specified in Section 3 and to produce a set of software engineering documents to demonstrate:
1. You understand the principles of software engineering methodologies,
2. You are capable of selecting and applying appropriate software engineering techniques, and
3. You have the skills to use advanced software engineering tools.

## 3. Tasks to do

The following specifies the tasks to be completed in this coursework and the distribution of marks in the assessment. A more detailed marking scheme is given in the file CHC6173-CW-Detailed Marking Scheme, which is also available on the student website.
### Task 0: Organisation of the Team and Project Management

The students are required to form a team themselves with four members from the class. The team must set up a management scheme and a collaboration mechanism, and work closely throughout the whole semester as a software engineering project.

Each team must set up a GitHub repository for the coursework project to host the documents of the project.

The team must meet regularly (for example, at least once a week) on fixed days and times. Each meeting should have an agenda before the meeting and a minute to record the meeting contents, especially the attendance at the meeting, progress since the previous meeting, a list of actions to take place and issues to be solved. The meeting agendas and minutes must be uploaded to GitHub immediately after it is created.

Each member of the coursework team must be responsible for the development of one of the following subsystems:
1. *AutoCare-Owner*: A subsystem for vehicle owners to register, book services, track repair status, and make payments.
2. *AutoCare-Workshop*: A subsystem for mechanics to manage diagnostics, repairs, and service updates.
3. *AutoCare-ServiceDesk*: A subsystem for mechanics to manage diagnostics, repairs, and service updates.
4. *AutoCare-Inventory*: A subsystem for parts suppliers to manage spare parts, stock levels, and orders.

***Note:*** The members of the team should work on different subsystems, while the whole team should develop a coherent system where the subsystems interact with each other.

Each subsystem will inevitably have two parts: one part on the user’s computer or mobile device and another part running on servers in the cloud. The parts on the Cloud that belong to different subsystems should be properly integrated so that they interact with each other to enable functions to deliver to various types of users.  Moreover, there may well be components running on the Cloud common to more than one subsystem and/or do not belong to any specific subsystem. The team should also work together to perform the software engineering activities to develop such common components.

### Task 1: Specification and Modeling Software Functional Requirements (20 Marks)

In this task, you will work as a requirements analyst in the project to produce a UML model of the software system to be developed using a software modeling tool. The UML model should contain the following types of models.  

(a) *Use Case Model* (10 Marks, Individual effort): Each member of the team should develop one Use Case Diagram to define the use cases of the subsystem to specify the scope of the software engineering project.  

(b) *Activity Model* (10 Marks, Individual effort): Each team member should select one use case of your subsystem to produce one Activity Diagram for the selected use case to specify the interactions between a user and the subsystem.

### Task 2: Software Architectural Design (30 Marks)

In this task, you will work as a software architect to produce an ***Architectural Design*** of the system in the *microservices architectural style*. The design should be at two different abstraction levels as follows.  

(a) *Architecture of the subsystem* (15 Marks, Individual effort): Each member of the team should produce an architectural design of your subsystem with focus on the microservices your subsystem provides and the microservices that your subsystem requests and other subsystems provide.  

(b) *Architecture of the whole system* (15 Marks, Team effort): The team should produce an architectural design of the whole system by integrating the subsystems.  

***Note****:*  
a. *You should specify the architectural designs in the UML component diagrams with a set of component nodes to represent microservices and a set of interfaces to represent the connectors between them.*  
b. *The components and connectors, including their methods and parameters, should be specified in a textual documentation to define their functionalities and meanings.*  
c. *In this part of the design, you are not required to give the internal structure of the components and connectors.*  

### Task 3: Software Detailed Design (20 Marks)

In this task, you will work as a software designer to produce a ***Detailed Design*** of the system for object-oriented implementation of the components (i.e. the *microservices*) in your *architectural design* of the subsystem. The design should specify the components from both structural and behavioural aspects in UML.  

(a) *Structural Model* (10 Marks, Individual effort): Each student should **select one component** in the architectural design of your subsystem and develop a Class Diagram to define the structure of the component.  
***Note***:  
a. *The selected component must be in the architectural model of your subsystem, but not in any other subsystems.*  
b. *The UML class diagram must contain the classes and relationships between them. You must give the attributes and methods of the classes.*  

(b) *Behavior Model* (10 Marks, Individual effort): Each student should produce a Sequence Diagram for the same component selected in Task 3(a) to define the dynamic behavior of the component.  
***Note****:*  
a. *The sequence diagram should specify the internal process of the interactions between the objects inside the component. It must be consistent with the structural model that you produced in Task 3(a).*  
b. *The behavior model must cover all possible scenarios of the operations of the component using advanced modeling facilities such as frames.*  

### Task 4: Software Testing (30 Marks)

In this task, you will work as a software quality engineer to develop a ***Software Test Plan***. Your test plan should consist of two parts:

(a) *Unit test plan* (15 Marks, Individual effort): You should select one microservice in your subsystem to develop a unit test plan.  
***Note***:  
a. *The unit test plan should aim at adequate testing of the same component (i.e. one microservice) that you have developed the structural model in Task 3(b).*  
b. *It should include a set of test cases that adequately cover all services and corresponding responses of the selected microservice.*  

(b) *System test plan* (15 Marks, Individual effort): You should select one use case to develop a system test plan.  
***Note****:*  
a. *The system test plan should aim at testing your subsystem on the same use case that you selected in Task 1(b).*  
b. *It should contain test cases that cover all different scenarios of the use case.*

## 4. Submission of Coursework

### 4.1 When to submit

The submission deadline is at <b>23:59 on (December 30<sup>th</sup>, 2026)</b>.

### 4.2 What to submit

Each group should submit one compressed (zip) file that contains a set of files listed in the table below. The file names and their contents to be included in the coursework submission must follow the convention given in the table below.  
***Note****: The text in <span style="color: red"><i>red</i></span> ink below should be replaced by your coursework group number.*

<center>Table 1. Files to be included in submission</center>

| **File name**                                           | **Format** | **Example**                                             | **Content**                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------------------- | ---------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CHC6173\_CW\_<span style="color: red">Gxx</span>.zip    | Zip file   | CHC6173\_CW\_<span style="color: red">G01</span>.zip    | The zip file should contain all the files of the coursework submission, where <span style="color: red">Gxx</span> is your coursework group number.                                                                                                                                                                                                                       |
| Cover\_<span style="color: red">Gxx</span>.pdf          | PDF        | Cover\_<span style="color: red">G01</span>.pdf          | The standard group coursework cover page.                                                                                                                                                                                                                                                                                                                                |
| TeamPart\_<span style="color: red">Gxx</span>.pdf       | PDF        | TeamPart\_<span style="color: red">G01</span>.pdf       | It should contain the work of Task 2(a), i.e. the architectural design of the whole system, including the UML component model and the textual documentation of the design.                                                                                                                                                                                               |
| Member\_<span style="color: red">Gxx_StdNum1</span>.pdf | PDF        | Member\_<span style="color: red">G01_1900001</span>.pdf | The work of student <span style="color: red">1900001</span>, including one UML use case diagram, one UML activity diagram, one architectural design of the subsystem in UML component diagram, one UML class diagram for one component of the subsystem, one UML sequence diagram for the same component of the subsystem, one unit test plan, and one system test plan. |
| Member\_<span style="color: red">Gxx_StdNum2</span>.pdf | PDF        | Member\_<span style="color: red">G01_1900002</span>.pdf | The work of student <span style="color: red">1900002</span>; _See above._                                                                                                                                                                                                                                                                                                |
| Member\_<span style="color: red">Gxx_StdNum3</span>.pdf | PDF        | Member\_<span style="color: red">G01_1900003</span>.pdf | The work of student <span style="color: red">1900003</span>; _See above._                                                                                                                                                                                                                                                                                                |
| Member\_<span style="color: red">Gxx_StdNum4</span>.pdf | PDF        | Member\_<span style="color: red">G01_1900004</span>.pdf | The work of student <span style="color: red">1900004</span>; _See above._                                                                                                                                                                                                                                                                                                |

- Your files must be formatted as follows:
    - It must be word-processed in 11-point Arial font and single-spaced
    - All pages must be numbered
    - Margins must be 1 inch on top, bottom, and both left and right sides of the paper
    - All pages must in A4 size
    - Student numbers must be entered on the cover page and state which subsystem is developed by which student.
    - The files should not contain your name(s).

*Please note that you are required to cite the work of others used in your solution and include a list of references using the university recommended referencing style. Please refer to the university’s regulations on academic conduct and plagiarism. If you have used AI-powered tools, you must declare how you have used them in the coursework.* 

### 4.3 Where to submit

You must upload **one** zip file containing all components to the student website.

### 4.4 Feedback on your coursework

- Informal verbal feedback can be obtained from the lecturer during the delivery of the module during practical classes. The students are encouraged to show their work to the lecturer and seek comments and advice.
- Each component of the coursework has its own deadline for verbal feedback:

| **Part** | **Deadline**   |
| -------- | -------------- |
| Part 1   | End of week 6  |
| Part 2   | End of week 8  |
| Part 3   | End of week 10 |
| Part 4   | End of week 12 |

[chc-2026-cw-detailed-marking-scheme.xlsx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fchc-2026-cw-detailed-marking-scheme.xlsx&wdOrigin=BROWSELINK)

Source: [chc6173cw-specsep2026.docx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fchc6173cw-specsep2026.docx&wdOrigin=BROWSELINK)
