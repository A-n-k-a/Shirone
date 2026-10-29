---
title: "Week 4 Practical Exercise: Software Modeling"
published: 2026-10-27
publishedAt: 2026-10-27T09:45:00+08:00
description: "At the practical class, the students should work in groups of 3-4 persons on Part 1 of the exercise questions. The students should do the exercises in Part 2 before attending the practical class."
image: "./145215368.jpg"
tags: ["Practical"]
category: "Software Engineering"
draft: false
pinned: false
lang: en
---

At the practical class, the students should work in groups of 3-4 persons on Part 1 of the exercise questions. The students should do the exercises in Part 2 before attending the practical class.

## Part 1. Case Study

Consider the case study of Mobile Online Restaurant Booking System.
1. Use the UML language to develop a set of software requirements models as a semi-formal definition of the functional requirements of the system. In particular, you should develop the following UML diagrams.
    - One _Use Case Diagram_ to show the use cases of the system for all types of users;
    - A set of _Activity Diagrams_ to show how the users will interact with the system in various use cases;
    - One _Class Diagram_ to represent the overall logic structure of the system;
    - A set of generic _Sequence Diagrams_ that each represents the internal behavior of the system in one use case;
    - A set of _Behavioral State Machines_ that each represents the behaviors of one key type of objects (i.e. one class) of the system.
2. Check the consistency and completeness of your model.
3. Use a UML modeling tool (such as Papyrus with Eclipse IDE) to represent the diagrams.

## Part 2: Exercises

1. The following is a narrative description of the business process of a property agent. Draw a use case diagram to represent the functional requirements of an information system that supports the business process.

_A property agent provides the services of selling and buying houses to its customers. People who want to sell their houses sign a contract with the agent and provide information on their house. This information is kept in a database by the agent and a subset of this information is sent to the citywide and nationwide multiple listing services used by the agent. An agent works with two types of potential buyers. Some buyers have an interest in one specific house. In this case, the agent prints information about the houses that matches the buyer’s interest from its database. Other buyers seek the agent’s advice in finding a house that meets their needs. In this case, the buyer completes a buyer information form that is entered into a buyer database, and then the agent uses its information to search its database for houses that meet their needs. When a seller signs a contract with the agent, the information about the house for sale is also matched with information about its potential buyers stored in the database, and sent to the matched buyers. When a buyer want to buy a specific house, the agent also mediates between the seller and buyer in negotiating the price. When an agreement between a buyer and the seller is achieved, the seller pays the agent a commission fee. The agent then removes the information about the house from the listings and updates the database._

---

2. The following is a narrative description of the business process of organisation of conferences with regards to the submitting, reviewing and accepting papers. Draw an activity diagram to represent the activities performed by various actors involved in the process.

_The author completes an online form that requests the user to input author name, correspondence address, email and, title of paper. The system validates this data and, if correct, asks the author to submit the paper. The author then browses to find the correct paper on their system and submits it. Once received and stored, the system returns to the author a reference number for the paper. Authors may submit as many papers as they like to be considered for acceptance to the conference up until the deadline date for submissions. Papers are allocated to referees for assessment. They review each paper and submit to the system their decision. Once the programme organizer has agreed the decisions authors are informed by email. Accepted papers are then schedule to be delivered at a conference. This involves allocating a date, time and place for the presentation of the paper._

_**Hints**_**:**
1. You should use swimlanes to represent who is doing what.
2. An action may need to have two activities: one for the actor who performs the action and the other for the actors who performs a corresponding activity to receive the result.
3. You should also include objects passed between different actors.
4. The information that given in a narrative description may be incomplete. You need to discover what is missing during modelling.

---

3. The following is a use case description of the examination paper preparation support system. Draw a UML activity diagram according to the description.

_**Use case name**_: submit question

_**Participant**_: lecturer

_**Entry conditions:**_  
1. The question is ready and stored in a file  
2. The lecturer is assigned to the module

_**Exit conditions:**_  
1. The file is uploaded to the system
2. The module leader is notified of the availability of the question
3. The event is logged by the system

_**Flow of Events:**_  
1. The lecturer logs into the system by entering his/her username and password;
2. The system checks the username and password;
3. The system displays the list of modules of which he/she is the lecturer, module leader and/or internal examiner;
4. The lecturer selects a module and his/her role in the module as a lecturer;
5. The system prompts the user to enter the file name and location on his/her computer, and additional information if any;
6. The lecturer enters file name and location, and types in the additional information;
7. The lecturer submits the questions and the file is uploaded to the system;
8. The system saves the file;
9. The system confirms the success of uploading the file.
10. The system notifies the module leader of the submission of the questions.

_**Exceptional conditions and alternative flow of events:**_  
- _When the username and password is not correct:_
- 3.1: display error message, go back to step 1;
- _When the lecturer is not listed on the module:_
- 4.1: quit the system;

_**Special requirements:**_  
1. The file should be encrypted when transmitted from lecturer’s computer to the server
2. The notification of success in uploading the file should be within 20 seconds
3. The event should be recorded in a log file to contain the following information:
    1. name of the lecturer,
    2. date and time of the event,
    3. the name of the event (upload exam question),
    4. the file on the server that stores the questions.

---

4. For each of the following systems, draw a UML class diagram to represent the structural model of the system.

_(a) University:_  
_A university offers a number of degree programmes, which are classified into BSc (Hons) degree programme, MSc degree program and PhD degree programme. To teach students in various programmes, the university runs a number of course modules. A particular module could be acceptable to a program, or compulsory to a program, or not acceptable at all to the programme. Each BSc (Hons) degree programme contains a number of modules as acceptable or compulsory, which are classified into stage I modules, advanced modules and honours modules. For a student who studies a BSc (Hons) degree programme, in order to obtain the degree he/she must complete a study plan that consists of at least 8 stage I modules, 16 advanced/honours modules and 4 honours modules that are acceptable to the programme._

_(b) Hotel:_  
_A hotel has a number of rooms that can be rent by guests. There are also a number of bathrooms, which are either connected to a specific room or are used to service multiple rooms on the floor. The rooms are classified into three types: single rooms, double rooms and family rooms. Each single room can only be rent to at most one guest. Each double room can be rent to at most two guests. Each family room can be rent to a family of up to two adults and two children._

_(c) IT Department:_  
_An IT company employs a number of employees. Each employee belongs to one department. Each department controls a number of projects. The employees may work on a number of projects. The employees include programmers, project managers, testers, analysts, and designers. Each project must be developed by a development team that consists of at least one manager, a number of programmers and testers, and may have one designer or analyst._

---

5. A computerized Theatre Booking System allows people to purchase tickets for shows at a theatre from one of many automated kiosks throughout a city. The kiosk will allow a user to choose a show, performance times and specific seats; pay by credit card and print the tickets. Kiosks are connected to a central box office computer-server containing a database of all shows and bookings.<br>Draw a sequence diagram showing the messages that pass between such objects as the **kiosk**, **box office** computer-server and **credit card service**, when an attempt is made to purchase a ticket for a show.

---

6. A travel authorization form is used in many companies to approve travel expenses for employees. The following is a description of the process in which a travel expense approval form is created, processed and finally filed and the case closed. Draw a behavioural state machine to represent the processing of travel authorization forms.

A travel authorization form is used by a company to approve travel expenses for employees. Typically, an employee fills out a blank form and sends it to his/her boss for a signature. If the amount is fairly small (£300), then the boss signs the form and routes it to the finance department to make a payment to the employee. The finance department then cuts a cheque that is sent to the employee for the right amount, and after the check is cashed, the form is filed away with the cleared cheque. If the cheque is not cashed within 90 days, the travel form expires. When the amount of the travel expenses is large (>£300), then the boss signs the form and sends it to the CFO, along with a paragraph explaining the purpose of the travel; the CFO signs the form and passes it along to the finance department. Of course, both the boss and the CFO can reject the travel authorization form if they do not feel that the expenses are reasonable. In this case, the employee can change the form to include more explanation or decide to pay the expenses by him/her-self.

---

7. Consider the situation about sending a Christmas card to a friend in a foreign country. Describe the process that the card goes through to get from your initial creation to being read by your friend, from the card’s perspective. Draw a behavioural state machine that depicts the states that the card moves through.

---

8. The activity diagram given below shows the interaction between a patient and a receptionist in making an appointment. Assume that the following objects/classes are used by the receptionist in this business process.
    - Patient List – an object that lists all registered patients of the clinic;
    - Paid Bills – an object of class Bill that records all paid bills;
    - Unpaid Bill – an object of the class Bill that records all unpaid bills;
    - Appointment Form – an object that records all the information about a patient’s appointment with a doctor.

Draw a sequence diagram to represent business process at logic level.

Source: 
<a href="/obu/level6/software-engineering/week4/CHC6173-2022-Practical%204%20-%20Software%20Modelling.docx" class="office-preview">
  CHC6173-2022-Practical 4 - Software Modelling.docx
</a>

<script>
document.querySelectorAll("a.office-preview").forEach((link) => {
  const fileUrl = new URL(
    link.getAttribute("href"),
    window.location.href
  ).href;

  const previewUrl = new URL(
    "https://view.officeapps.live.com/op/view.aspx"
  );

  previewUrl.searchParams.set("src", fileUrl);

  link.href = previewUrl.href;
  link.target = "_blank";
  link.rel = "noopener noreferrer";
});
</script>
