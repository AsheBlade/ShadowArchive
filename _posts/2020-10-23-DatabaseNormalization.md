---
layout: post
title: Database Normalization
date: 2020-10-23
author: Shadow Walker
tags: [SQL, Database]
toc: true
comments: true
---

## 1NF

- should be not repeating groups of columns.


This is the simpliest one. Here is an example with repeating columns: 
![](https://www.essentialsql.com/wp-content/uploads/2014/06/FirstNormalFormUnormalize.png)

## 2NF

- The table is in 1st normal form
- All the non-key columns are dependent on the table’s primary key.

Explain: 

 When we talk about columns depending on the primary key, we mean, that **in order to find a particular value, such as what color is Kris’ hair, you would first have to know the primary key, such as an EmployeeID, to look up the answer.**

## 3NF

- A table is in 2nd normal form.
- It contains only columns that are non-transitively dependent on the primary key. 

This is a little bit hard to understand. It basically is used to remove unnecessary colunmns. In the example shows below, CustomCity depends on CustomerPostalCode. 



![](https://www.essentialsql.com/wp-content/uploads/2014/08/ThirdNormalFormIssues.png)


We fix this by remove CustomCity from CustomerID and create a new entity called PostalCode with city inside. 

![](https://www.essentialsql.com/wp-content/uploads/2014/08/ThirdNormalFormDataModel.png)

## More resource

All above are from [here](https://www.essentialsql.com/get-ready-to-learn-sql-11-database-third-normal-form-explained-in-simple-english/). 