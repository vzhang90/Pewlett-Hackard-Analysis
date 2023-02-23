# Pewlett Hackard Analysis
Pewlett Hackard is a large company boasting several thousand employees, but baby boomers are beginning to retire at an unprecedented rapid rate *(leaving thousounds of job openings)*. As the company tries to look towards the future, it wants to anticipate retirement packages for those who meet a certain criteria while considering which positions will need to be filled in the near future.

***This report's analysis will:  1) determine the number of retiring employees per title  &  2) identify employees who are eligible to participate in a mentorship program***

## Overview of Analysis

In order to address concerns around Pewlett Hackard's coming and eventual "silver tsunami," six CSV files will be analyzed using SQL to build an employee database.

> **Resources:** 
> 1) [departments.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/departments.csv)
> 2) [dept_empt.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/dept_emp.csv)
> 3) [dept_manager.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/dept_manager.csv)
> 4) [employees.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/employees.csv)
> 5) [salaries.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/salaries.csv)
> 6) [titles.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/titles.csv)

<sub>using [Quick DBD](https://www.quickdatabasediagrams.com/) can help model the data through ERDs conceptually, logically, and physically</sub>
  
---

### The Number of Retiring Employees by Title
**Retirement Titles Table**
- A ***SQL query*** in pgAdmin is written and executed to create a **Retirement Titles table** for employees who are born between January 1, 1952 and December 31, 1955:
    - retrieves the `emp_no`, `first_name`, and `last_name` columns from the **Employees table**
    - retrieves the `title`, `from_date`, and `to_date` columns from the **Titles table**
    - creates a new table using the `INTO` clause
    - joins both tables on the primary key
    - filters data on `birth_date` column to retrieve employees who were born between 1952 and 1955 
        - orders by the employee number


---

### The Employees Elegibile for the Mentorship Program
- A query is written and executed to create a Mentorship Eligibility table for current employees who were born between January 1, 1965 and December 31, 1965:

## Results

## Summary
- How many roles will need to be filled as the "silver tsunami" begins to make an impact?
- Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?

provide two additional queries or tables that may provide more insight into the upcoming "silver tsunami." 
