# Pewlett Hackard Analysis
Pewlett Hackard is a large company boasting several thousand employees, but baby boomers are beginning to retire at an unprecedented rapid rate *(leaving thousounds of job openings)*. As the company tries to look towards the future, it wants to anticipate retirement packages for those who meet a certain criteria while considering which positions will need to be filled in the near future.

This report's analysis will:  
***1. determine the number of retiring employees per title*** 
***2. identify employees who are eligible to participate in a mentorship program***

## Overview of Analysis

In order to address concerns around Pewlett Hackard's coming and eventual "silver tsunami," six CSV files will be analyzed using **SQL** query tool in **pgAdmin** to build an employee database.

> **Resources:** 
> 1) [departments.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/departments.csv)
> 2) [dept_empt.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/dept_emp.csv)
> 3) [dept_manager.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/dept_manager.csv)
> 4) [employees.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/employees.csv)
> 5) [salaries.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/salaries.csv)
> 6) [titles.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/titles.csv)

<sub>Planning out the relations between different datasets with [Quick DBD](https://www.quickdatabasediagrams.com/) can help model the data through ERDs conceptually, logically, and physically</sub>
  
---

### The Number of Retiring Employees by Title
**Retirement Titles Table**
This SQL query will:
1. retrieve `emp_no`, `first_name`, and `last_name` columns from employees table
2. retrieve `title`, `from_date`, and `to_date` columns from titles table
3. create new table called retirement_titles using `INTO` clause
4. join the Employees and Titles tables on primary key (`emp_no`)
5. filter data on `birth_date column` to retrieve employees born between 1952 & 1955 (order results by `emp_no`)
6. `DISTINCT ON` statement to retrieve most recent title of each employee
7. insert results into retirement_titles table
8. count number of retirement-age employees by most recent job title
9. order results by count in descending order
10. export retirement_titles table as a CSV file [retirement_titles.csv]()
  
**Unique Titles Table**
- A query is written and executed to create a **Unique Titles table** that contains the ***employee number***, ***first***and ***last name***, and ***most recent title***:
    - retrieves the ***employee number***, ***first*** and ***last name***, and ***title*** columns from the **Retirement Titles table**
    - uses the `DISTINCT ON` statement to retrieve first occurrence of employee number for each set of rows defined by the `ON ()` clause
    - excludes those employees that have already left the company by filtering on `to_date` to keep only those dates that are equal to `'9999-01-01'`
    - creates **Unique Titles table** using the `INTO` clause
    - sorts **Unique Titles table** by
        - *ascending* order by the ***employee number*** of most recent title
        - *descending* order by the ***last date*** (i.e., `to_date`) of most recent title
- The Unique Titles table is exported as `unique_titles.csv`

**Retiring Titles Table**
- A query is written and executed to create a **Retiring Titles table** that contains the ***number of titles filled by employees who are retiring:***
    - retrieves ***titles*** and uses `COUNT()` to retrieve the ***number of titles*** from the **Unique Titles table**
    - creates **Retiring Titles table** to hold required information
    - groups table by ***title***, then sort the count column in *descending* order
- The Ritiring Titles table is exported as `retiring_titles.csv`

---

### The Employees Elegibile for the Mentorship Program
- A query is written and executed to create a Mentorship Eligibility table for current employees who were born between January 1, 1965 and December 31, 1965:

In the [Employee_Database_challenge.sql file](), a query is written to create a Mentorship Eligibility table that holds the employees who are eligible to participate in a mentorship program.
    1. retrieve the `emp_no`, `first_name`, `last_name`, and `birth_date` columns from the Employees table
    2. retrieve the `from_date` and `to_date` columns from the Department Employee table
    3. retrieve the `title` column from the Titles table
    4. use a `DISTINCT ON` statement to retrieve the first occurrence of the employee number for each set of rows defined by the `ON ()` clause
    5. create a new table using the `INTO` clause.
    6. join the Employees and the Department Employee tables on the primary key
    7. join the Employees and the Titles tables on the primary key
    8. filter the data on the `to_date column` to all the current employees, then filter the data on the `birth_date` columns to get all the employees whose birth dates are between January 1, 1965 and December 31, 1965
    9. order the table by the employee number
    10. export the Mentorship Eligibility table as `mentorship_eligibilty.csv`

## Results

## Summary
- How many roles will need to be filled as the "silver tsunami" begins to make an impact?
- Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?

provide two additional queries or tables that may provide more insight into the upcoming "silver tsunami." 
