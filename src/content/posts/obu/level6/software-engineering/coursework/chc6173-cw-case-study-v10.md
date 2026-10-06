---
title: "CHC6173 Software Engineering Coursework Case Study"
published: 2026-09-27
description: "Requirements Definition of AutoCare: A Multi-Subsystem Vehicle Service and Maintenance Management Platform"
image: "./144580831.jpg"
tags: ["Coursework", "Case Study"]
category: "Software Engineering"
draft: false
pinned: false
lang: en
---

<center><h2>Oxford Brooks University</h2></center>  
<center><h2>CHC6173 Software Engineering<br>Coursework Case Study</h2></center>  
<center><h3>Requirements Definition of AutoCare: A Multi-Subsystem Vehicle Service and Maintenance Management Platform</h3></center>  
<center><h5>Mohamed Aymen Chebira<br>
Department of CS/SE<br>
Chengdu University of Technology<br>
Email: aymen.chebira@zy.cdut.edu.cn
</h5></center>

## 1. Introduction

With the increasing complexity of modern vehicles and the growing demand for efficient service management, digital platforms can significantly improve how vehicle maintenance services are delivered. A new generation of **vehicle service management systems** can integrate customer interactions, workshop operations, inventory control, and administrative functions into a unified cloud-based solution.

A software company, **AutoSoft Ltd**, has decided to develop a system called **AutoCare**, which is a multi-subsystem platform designed to modernize vehicle servicing and maintenance operations. The system aims to streamline service booking, repair tracking, parts management, and operational control while improving customer experience and service efficiency.

This document defines the functional requirements of the system. The remainder of the document is organized as follows. Section 2 describes the targeted user types. Section 3 outlines the key design features. Section 4 provides the functional requirements grouped by user type.

## 2. Types of Targeted Users 

The main types of users of the system will be:
1. *Vehicle Owners – Customers who book services, track repairs, and manage their vehicles.*
2. *Mechanics – Staff who diagnose, repair, and update service tasks.*
3. *Service Advisors – Staff who manage bookings, communicate with customers, and coordinate services.*
4. *Parts Suppliers – External or internal staff responsible for providing and managing spare parts.*
<a id="_Ref177389978"></a>
## 3. Key Design Features

The *AutoCare* system consists of the following subsystems; all connected to services running on the cloud:
1. *AutoCare-Owner: A subsystem for vehicle owners to register, book services, track repair status, and make payments.*
2. *AutoCare-Workshop: A subsystem for mechanics to manage diagnostics, repairs, and service updates.*
3. *AutoCare-ServiceDesk: A subsystem for service advisors to handle bookings, customer communication, and scheduling.*
4. *AutoCare-Inventory: A subsystem for parts suppliers to manage spare parts, stock levels, and orders.*

## 4. Specification of Functional Requirements

### 4.1 *Requirements of Vehicle Owners*

**FR-VO-1: Register as Vehicle Owner**. The system should allow individuals to register, storing details such as name, address, email, phone, vehicle details(Registration Number, Make, Model, Year of Manufacture) and login credentials.  
**FR-VO-2: Manage Vehicle Profile.** The system should allow owners to add, update, and remove vehicle information.  
**FR-VO-3: Book Service Appointments.** The system should enable owners to schedule service appointments by selecting date, time, and service type.  
**FR-VO-4: Track Service Status.** The system should provide real-time updates on the status of vehicle servicing and repairs.  
**FR-VO-5: Make Payments.** The system should support secure online payment for services and parts.  
**FR-VO-6: Authentication.** The system should allow vehicle owners to log in and log out securely to access their accounts.  

### 4.2 *Requirements of Mechanics*

**FR-M-1: View Assigned Tasks**. The system should allow mechanics to view assigned service and repair tasks.  
**FR-M-2: Update Repair Status.** The system should enable mechanics to update the progress of repairs (e.g. pending, in progress, completed).  
**FR-M-3: Request Parts.** The system should enable mechanics to request required spare parts for repairs.  
**FR-M-4: Record Completed Work.** The system should support librarians in assisting members with resource searches.  
**FR-M-5: Authentication.** The system should allow authorized mechanics to log in/out to the workshop dashboard.  

### 4.3 *Requirements of Service Advisors*

**FR-SA-1: Manage Bookings.** The system should allow service advisors to create, update, and cancel service appointments.  
**FR-SA-2: Assign Tasks to Mechanics.** The system should enable assigning service jobs to available mechanics.  
**FR-SA-3: Communicate with Customers.** The system should support sending updates and notifications to vehicle owners.  
**FR-SA-4: Manage Service Schedule.** The system should provide a scheduling interface to manage daily service workload.  
**FR-SA-5: Authentication.** The system should allow authorized service advisors to log in/out to the service desk interface.  

### 4.4 *Requirements of Parts Suppliers*

**FR-PS-1: Manage Inventory**. The system should allow tracking and updating spare parts inventory levels.  
**FR-PS-2: Process Parts Requests.** The system should enable receiving and fulfilling parts requests from mechanics.  
**FR-PS-3: Update Stock Levels.** The system should automatically update stock levels after transactions.  
**FR-PS-4: Manage Supplier Orders.** The system should support placing and tracking orders to external suppliers.  
**FR-PS-5: Authentication.** The system should allow authorized parts suppliers to log in/out to the inventory system.  

Source: [chc6173-cw-case-study-v10.docx](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fvle.zycdut.net%2Fsites%2Fstudent.zy.cdut.edu.cn%2Ffiles%2Fattachments%2Fchc6173-cw-case-study-v10.docx&wdOrigin=BROWSELINK)
