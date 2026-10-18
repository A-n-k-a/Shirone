---
title: "Practical 2 Exercise Questions"
published: 2026-10-13
publishedAt: 2026-10-13T09:00:00+08:00
description: "This exercise is designed to enhance your understanding of the key concepts and the knowledge of processes and key techniques of software project management."
image: "./88427255.jpg"
tags: ["Case Study"]
category: "Software Engineering"
draft: false
pinned: false
lang: en
---

## Part I. Group Work at Practical Class

Work in a group of 3-4 students at the practical class on the following 2 exercises. 

### Exercise 1: Risk Analysis

Consider the project of Mobile Restaurant Booking System (see Case Study of [week 1](../../week1/seminar/)). 
1. Identify the risks associated to the project.
2. Assess the risk by estimate the likelihood of occurrence and the potential consequences.
3. For each risk, propose some risk prevention/avoidance and risk impact minimization means.
***Hint***: This is the same question of Exercise (7) that you should have done in the previous week after the class. 

### Exercise 2: Project Planning

Develop a project plan for Mobile Restaurant Online Booking System.
1. Identify the tasks of the project and decompose the tasks into a list of activities of manageable sizes.
2. For each activity of the list, define the outcomes and inputs.
3. Determine the dependences between the activities.
4. Estimate the time duration needed to conduct each activity.
5. Draw a Pert chart for the activities and work out the earliest start time and latest finish time for each activity.
6. Develop a schedule for the project based on the results of Pert chart modeling of project process.

## Part II. Individual Work

Do the following 2 exercises after the practical class. 

### Exercise 3: Constructing a PERT Chart

The following is a simplified list of tasks for the development of a computer application with information about the dependences among the tasks and the time duration required to perform the tasks. Draw a Pert chart according to the data, calculate the earliest start time and the latest finish time for each task, and identify the critical paths. 

| ACTIVITY                    | DURATION (Weeks) | DEPENDS ON  |
| --------------------------- | ---------------- | ----------- |
| 10 Architectural Design     | 2                |             |
| 15 Install open source code | 3                |             |
| 20 Test open source code    | 6                | 15          |
| 25 Test infrastructure      | 2                | 20          |
| 30 Install database system  | 2                | 10          |
| 40 Create data files        | 5                | 30          |
| 50 Write operation manual   | 3                | 40          |
| 60 Write program specs      | 4                | 10          |
| 70 Program coding           | 12               | 60          |
| 80 Integration test         | 6                | 25, 70, 40  |
| 90 Acceptance test          | 2                | 10          |
| 100 User training           | 5                | 90          |
| 110 Handover                | 2                | 100, 80, 50 |

### Exercise 4: Constructing a Gantt Chart

Based on your results of Exercise 3, develop a schedule for the project and present your schedule in the form of a Gantt chart. 

***Hint***: Assume that you have enough resource to carry out tasks always at the earliest possible times. 

Source: 
<a href="/obu/level6/software-engineering/week2/CHC6173-2021-Practical%202%20-%20Project%20Management.docx" class="office-preview">
  CHC6173-2021-Practical 2 - Project Management.docx
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
