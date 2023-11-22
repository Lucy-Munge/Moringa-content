# One-to-Many and Many-to-Many Joins - Lab

## Introduction

In this lab, you'll practice your knowledge of one-to-many and many-to-many relationships!

## Objectives

You will be able to:

* Explain one-to-many and many-to-many joins as well as implications for the size of query results
* Query data using one-to-many and many-to-many joins

## One-to-Many and Many-to-Many Joins
<img src='images/Database-Schema.png' width="600">

## Connect to the Database

Include the relevant imports, then connect to the database located at `data.sqlite`.


```python
# Your code here
```

## Employees and Their Offices (a One-to-One Join)

Select all of the employees including their first name and last name along with the city and state of the office that they work out of (if they have one). Include all employees and order them by their first name, then their last name.


```python
# Your code here
```

## Customers and Their Orders (a One-to-Many Join)

Select all of the customer contacts (first and last names) along with details for each of the customers' order numbers, order dates, and statuses.


```python
# Your code here
```

## Customers and Their Payments (Another One-to-Many Join)

Select all of the customer contacts (first and last names) along with details for each of the customers' payment amounts and date of payment. Sort these results in descending order by the payment amount. 


```python
# Your code here
```

## Orders, Order Details, and Product Details (a Many-to-Many Join)

Select all of the customer contacts (first and last names) along with the product names, quantities, and date ordered for each of the customers and each of their orders. Sort these in descending order by the order date.

> Note: This will require joining 4 tables! This can be tricky! Give it a shot, and if you're still stuck, turn to the next section where you'll see how to write subqueries that can make complex queries such as this much simpler!


```python
# Your code here
```

## Summary

In this lab, you practiced your knowledge of one-to-many and many-to-many relationships!
