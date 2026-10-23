---
title: "Case Study: Mobile Restaurant Booking System"
published: 2026-10-20
publishedAt: 2026-10-20T09:00:00+08:00
description: "This document first reviews the target user types of the system and the key features to be realised. It then defines the functional requirements of the system."
image: "./150951600.png"
tags: ["Case Study"]
category: "Software Engineering"
draft: false
pinned: false
lang: en
---

### Functional Requirements

#### 1. Introduction

With the advent of mobile and cloud computing technologies, it is perceived that the traditional telephone booking and online booking of restaurant tables can be revolutionised by developing a mobile application that links to a back-end cloud computing system delivering functionality in the form of Software-as-a-Service (SaaS). The CloudSoft [+CloudSoft] Ltd thus decided to develop such a system to realise advanced functions of restaurant table booking. It is perceived to consist of three parts: (a) a mobile app for running on smart phones for restaurant customers, (b) a web interface for running on desktop or tablet computer for restaurant managers and staffs, and (c) a back-end software system running on a server for system operators to perform operation across restaurants and to store information.

This document first reviews the target user types of the system and the key features to be realised. It then defines the functional requirements of the system.

[+CloudSoft]: This is a fictional company specializes in the development of computer application systems.

#### 2. Types of Targeted Users

The main types of the users of the system will be:
1. _Restaurant Managers_. They are the persons who run the restaurants. They will use a desktop computer with a web-based interface to setup and update the restaurant’s website.
2. _Restaurant Customers_. They are the customers of restaurants. They are usually from the general public and anonymous to the restaurants. They will use a mobile app to search restaurants, book tables, and order/pre-order food, and make comments on the restaurant.
3. _Restaurant Service Staff_. They are the employees of a restaurant and provide various services to the customers. They will use a tablet computer in the restaurant to assist their services to the customers.
4. _System Operators_. They are staff members of CloudSoft. They will use a desktop computer with a web-based interface to manage the whole system and provide services that across the individual restaurants.

#### 3. The Required Key Design Features of the System

The following are the key design features that the system must realise.

**KF-1: Dynamic Update of Information.** The system should realise quick dynamic update the state of the restaurants, including information about the availability tables/seats in real time, availability of the food, etc. Dynamic update of information has been recognised as one of the killer features of this system that distinguishes it from static web sites of restaurants.

**KF-2: Services Across Restaurants.** Another killer feature of the system is that it should provide those services across individual restaurants, such as the favourable dishes and menus over all restaurants, the discount vouches and royalty points for use at any restaurants on this system, etc. This relies on collecting a lot of data from a large number of participating restaurants.

**KF-3: Seamless Process.** It is important to connect all components together to make the activities of searching, booking, ordering, paying bill, and commenting a continuous effortless and seamless process. For example, viewing a favourable menu or dish should be linked to pre-order/order the dish or menu with one click of button. The process of different types of users must be integrated seamlessly, too.

**KF-4: User-friendly HCI.** The system should provide apps for restaurant customer users running on various mobile phone/device platforms with graphic user interface. It should also provide user friendly HCI for Restaurant Managers, Service Staffs and System Operators. It should enable pictures of the food be associated to the menus, pictures of the rooms and surrounding environment be uploaded to the website, etc.

#### 4. Functional Requirements of the System

The functional requirements of the system are grouped according to the types of users.

##### 4.1 _Requirements of Restaurant Managers_

**FR-RM-1: Setup Restaurant Website**. The basic requirements from a _Restaurant Manager’s_ point of view is that the system should be able to support setting up a customised web interface of a restaurant, which should contains the following types of information of the restaurant:
- _basic data_, such as name and address, opening hours, and type of cuisines, location and directions, etc.
- _menus_, such as the types and prices of the dishes, nutrition and allergic data, images of the food, etc.
- _space_, such as the number of tables/seats available, the layer out and images of the rooms, the site and its environment, parking spaces, etc.;
- _staff_, such as the chef’s qualification and experiences, and service personnel, etc.

**FR-RM-2: Update Restaurant Information**. Some of the restaurant information may change dynamically. For example, there may be menus of “_Today’s Special_”, which need to be updated daily. Thus, the system must provide a facility to enable the restaurant manager’s to update his/her restaurant’s information.

##### 4.2 _Requirements of Restaurant Customer_

**FR-RC-1: Search for Restaurants.** The basic requirements from _Restaurant Customers_’ point of view is that the system should be enable the customers to use a smart phone app to search for restaurants of certain conditions, such as restaurant of a certain name, at a certain location, within a certain distance of the customer’s current location, serves a certain type of food, and with a certain number of available tables/seats, within a certain price ranges, etc.

**FR-RC-2: Booking A Table.** Once a desired restaurant is found, the system should enable the customers to book a table for a given number of seats at certain time. The system should enable the customers to view the room layout and the see the availability of the tables and make reservation of a table at certain time if it is available.

**FR-RC-3: Pre-Order of Food.** Once a customer reserves a table successfully, the system should enable the customer to make pre-order of food online before arriving at the restaurant and specify a time of arrival at the restaurant.

**FR-RC-4: Customer Feedback.** The system should enable the customer to give feedback and comments on the food and service that they received in a restaurant using their smart phone app. The feedback facility should enable the customers to enter text comments on a restaurant and/or a food, to give scores on various aspects, and to upload images taken by the smart phone. The customer feedbacks should be publically accessible on the web.

##### 4.3 _Requirements of Restaurant Service Staff_

**FR-RS-1: Check-In Pre-Booked Customer**. When a customer arrives at the restaurant, the system should enable restaurant service staff to check the customer’s table booking, and if the customer has a valid booking of a table, the system should display the booking information to allow the service staff to allocate the table to the customer and change the table state to “occupied” and booking state to be “fulfilled”.

**FR-RS-1: Check-In Un-booked Customer**. When a customer who has no booking of a table arrives at the restaurant, the system should enable restaurant service staff to looking for a table that is available and allocate the table to the customer. The system should change the table state to “occupied”. Once a table is assigned, it will become unavailable for booking.

**FR-RS-2: Order Food.** The system should allow the service staff to take order of food and drink from the customer in the restaurant. The order should be automatically submitted to the kitchen for the chef to prepare and cook the food.

**FR-RS-3: Activate Pre-Order.** When a customer who made a pre-order arrives at the restaurant, the system should be able to activate the pre-order, and possibly revise the pre-order.

**FR-RS-4: Trace States of Services.** The system should be able to help the staff to trace the state of services to the customers, including whether an order of food is cooked or served, whether a booking of table is fulfilled, and whether a table is booked for how many seats so that the table to be laid accordingly.

**FR-RS-5: Take payment.** The system should be enable the staff to display/print out the bill and take payments from the customers to settle the bill.

##### 4.4 _Requirements of System Operators_

**FR-SO-1: Activate/Deactivate Restaurant’s Account.** The system should enable the system operators to activate/deactivate a restaurant’s account. Once a restaurant’s account become active, the restaurant’s manager should be able to setup and update its website.

**FR-SO-2: Statistical Analysis of Data.** The System should provide various statistical data to the public and/or the restaurant owners, such as the star ratings by the customers, the most favourable dishes of food, the most favourable menus (i.e. combinations of dishes), the average cost per person, average time to wait before food is served, etc.

**FR-SO-3: Organise Cross-restaurant Promotional Events.** The system should enable system operators to organise promotional events across restaurants, such as a Food Festival, Pancake Day, Christmas and New Year Party, etc.

**FR-SO-4: Social Networking.** The system should provide a social networking facility for the customers to form a virtual community in order to enable them to organise parties, and to recommend restaurants, food, and menus to each other. It should also provide convenient links to popular social networking systems, such as Facebook, Twitter, WeChat, etc.

**FR-SO-5: Customer Data Management.** The system should establish and maintain a database of the customers to record their bookings, orders and feedbacks, etc., and to develop an incentive mechanism for attracting the customers, through royalty points, discount vouches, etc.

Source: 
<a href="/obu/level6/software-engineering/week3/CHC6173-Practical%203%20-%20Case%20Study%20-%20Functional%20Requirements%20of%20A%20Mobile%20Resturant%20Booking%20System.docx" class="office-preview">
  CHC6173-Practical 3 - Case Study - Functional Requirements of A Mobile Resturant Booking System.docx
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

