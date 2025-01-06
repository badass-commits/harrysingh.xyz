---
layout: project
title: car-inventory
date: 2021-04-26 15:56:42 -0400
category: projects
tags: java mysql
---

![Inventory Search](/assets/images/projects/car-inventory/screenshots/InventorySearch.png)

## Summary

One of the required courses for Computer Science was `Software Engineering`. This course basically was a crash course in how software development and computer science are not synonymous. As a part of this course, we were required to work in groups to write and present a piece of software that showed we used source control, architectural design patterns, and teamwork. For the semester I took this course, we were asked to write a car inventory management application.

This project has always stuck out to me as something I wanted to take a look at later and apply the knowledged I've learned since the original project.

## Technical Notes

My group and I wrote our application in Java, using a MySQL database to store the cars and related information. We used an MVC architecture, although being students there was some blurring of lines between layers. As a part of my refactor, I made the project into a Maven project and added a MySQL container with an `init.sql` script.

The tables that were in our database included:

| Name          | Description                                                                                          |
| ------------- | ---------------------------------------------------------------------------------------------------- |
| Car           | contains all of the information about one specific car                                               |
| Customer      | can buy cars                                                                                         |
| CarHistory    | contains the list of events in a car's history(must contain at a minimum: the entry into the system) |
| CustomerOrder | relates a customer to a car that they have ordered                                                   |

![car-inventory Entity Relationship diagram](/assets/images/projects/car-inventory/CarInventoryERdiagram.png)

_Note: I use improved entity-relationship names in this diagram, see below._

I'm not sure if we used foreign key constraints in the original, but since nothing is deleted and the benefits of FKC are debated I decided not to use them in the new schema I wrote.

## Screenshots

![Add Car](/assets/images/projects/car-inventory/screenshots/AddCar.png)
_Enter new cars on the second tab._

![Vehicle Information](/assets/images/projects/car-inventory/screenshots/VehicleInformation.png)
_A vehicle's information and history is displayed when you click view on a selected car in the Search tab._

![Customers](/assets/images/projects/car-inventory/screenshots/CustomerScreens.png)
_The screens related to adding/selecting customers and submitting orders._

![Orders](/assets/images/projects/car-inventory/screenshots/Orders.png)
_View and search past orders._

## Lessons Learned

While refactoring this code, six years after writing it, some obvious lessons jumped out at me.

### 1. Domain Driven Design is critical when desgining an entity based system

This piece of software was basically just a way to manage a set of entites and their state and relationships. The `CarHistory` table really could have been called `Event` and the _relationship_ between `Car` and `Event` could be referred to as a _car's history_.

### 2. Staging and dev environments are important, doing them well even more so

I've been spoiled in my career in web development by the ease of spinning up dev envrionments using Docker and other tools like Skeema. When we originally wrote this, we had just one MySQL instance running on AWS. I'm not even sure if we ever really wrote down what the planned schema was or if we just made it once and made the rest of the code fit. When I was working on the refactor I actually had to reverse engineer a schema and write an `init.sql` file for Docker.

### 3. Raw SQL...

I know people have their opinions about ORMs and how important they are. I won't debate the merits or drawbacks of writing your own SQL statements as strings. But what I will say is that if you are going to do that, make sure you do it in one architectural layer, using a consistent pattern, and in a reusable way. Simple statement generators that requested certain columns from a table would have gone a long way in this project. While refactoring I ran into a bug where one car had multiple car history events of being added to the system, this should only happen once per car. It was not until I found some hidden SQL in a view that I realized that the `CarHistory` records were tracked by the `VIN` of the car and not the `ID` of the car. This totally makes sense but I had fat fingered a duplicate `VIN` and had no logic in my code nor a `UNIQUE` key in my schema to prevent adding cars with duplicate `VINs`
