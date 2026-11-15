---
title: "Week 6 Exercise: Software Design"
published: 2026-11-10
publishedAt: 2026-11-10T09:45:00+08:00
description: "The practical questions are intended to be an exercise of software design methods and techniques using different design strategies, and the presentation of your design at a high level of abstraction in UML."
image: "./42117013.jpg"
tags: ["Practical", "Software Design"]
category: "Software Engineering"
draft: false
pinned: false
lang: en
---

## Introduction

The practical questions are intended to be an exercise of software design methods and techniques using different design strategies, and the presentation of your design at a high level of abstraction in UML.

## Case Study

Use UML component, package and deployment diagrams to present your overall structural design of the *Mobile Restaurant Booking System*.  
***Hint***: Please follow the steps given below.  
1. You should start with a component diagram as a high-level model in which the subsystems and the cloud should be the components and wired together through ports and interfaces. The focus of the top-level model is on the interfaces between subsystems and the cloud.
2. After finishing this top-level model, you should revise it by adding components into each subsystem and add the components to run in the cloud. These components must also be wired together into a system. The components running on the cloud should be included those to receive service requests from mobile apps, to process the requests, to store data of the restaurants, the customers and their bookings, orders, payments, and rankings and feedbacks, and to send service results to the mobile apps.
3. The next step of refinement of your design is to put the classes into each component node in the component diagram. The classes that your put in the components should be those in the class diagram that you should have developed last week.
4. After the construction of the component model, you should then put classes in the components of a subsystem into a package and depicted this in a package diagram.
5. The deployment diagram should show how packages for each subsystem are to be deployed to different types of devices.

## Exercise of Software Design

Try to use different design strategies to design a program for the problems specified below. Present your design in UML component, package or deployment diagram.

A program is required to merge two (possibly empty) lists of contact addresses. Each element of the contact list consists of a name and an email address. The input lists are ordered alphabetically in the ascending order according to the names. The output list should also be ordered and for matching records the output list should contain that contact data only once.

Example:

| *input1*                       | *input2*                       | *input3*                       |
| ------------------------------ | ------------------------------ | ------------------------------ |
| Ball, fball@bournes.ac.uk      | Brownsey, kb@yahoo.com         | Ball, fball@bournes.ac.uk      |
| Brownsey, kb@yahoo.com         | Champion, bchampion@bt.co.uk   | Brownsey, kb@yahoo.com         |
| Champion, bchampion@bt.co.uk   | Dobbyn, dobbyn@open.ac.uk      | Champion, bchampion@bt.co.uk   |
| Lightfoot, david@brookes.ac.uk | Holmes, barry@holms.com        | Dobbyn, dobbyn@open.ac.uk      |
| Zajicek, mz@cs.taxes.edu       | Lightfoot, david@brookes.ac.uk | Holmes, barry@holms.com        |
| Zhu, hzhu@brookes.ac.uk        |                                | Lightfoot, david@brookes.ac.uk |
|                                |                                | Zajicek, mz@cs.taxes.edu       |
|                                |                                | Zhu, hzhu@brookes.ac.uk        |

After you finish the design for the problem, assess your design by considering each of the following situations that this program could be used, and, then to revise your design to make it suitable for the usage of the software, if necessary.  
1. The program is a part of a mobile App for managing contacts.
2. The program is a part of a cloud native application running on a cluster of servers. The mailing lists are so huge that they cannot be completely loaded into the memory of one server to process.
3. One of the lists is very large while the other is much smaller than the other.
4. There is a perceived modification of the software so that it will require to merge more than two mailing lists, potentially a large number of lists.

Source: 
<a href="/obu/level6/software-engineering/week6/CHC6173-Practical%206%20-%20Software%20Design.docx" class="office-preview">
  CHC6173-Practical 6 - Software Design.docx
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
