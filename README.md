# Pewlett Hackard Analysis
Pewlett Hackard is a large company boasting several thousand employees, but baby boomers are beginning to retire at an unprecedented rapid rate *(leaving thousounds of job openings)*. As the company tries to look towards the future, it wants to anticipate retirement packages for those who meet a certain criteria while considering which positions will need to be filled in the near future.

This report's analysis will:  
***1. determine the number of retiring employees per title***   
***2. identify employees who are eligible to participate in a mentorship program***

## Overview of Analysis

In order to address concerns around Pewlett Hackard's coming and eventual "silver tsunami," six CSV files will be analyzed:

> <sub>**Pewlett Hackard's employee datasets:**</sub>   
> <sub>1. [departments.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/departments.csv)</sub>  
> <sub>2. [dept_empt.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/dept_emp.csv)</sub>  
> <sub>3. [dept_manager.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/dept_manager.csv)</sub>  
> <sub>4. [employees.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/employees.csv)</sub>  
> <sub>5. [salaries.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/salaries.csv)</sub>  
> <sub>6. [titles.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/titles.csv)</sub>

*Planning out the relations between different datasets with [Quick DBD](https://www.quickdatabasediagrams.com/) can help model the data through ERDs conceptually, logically, and physically*

In the [Employee_Database_challenge.sql file](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/Queries/Employee_Database_challenge.sql), 

SQL queries are written and executed in **pgAdmin**, creating four tables to build an employee database exported as CSV files:
> 1. [retirement_titles.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/retirement_titles.csv)
> 2. [unique_titles.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/unique_titles.csv)
> 3. [retiring_titles.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/retiring_titles.csv)
> 4. [mentorship_elibigility.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/mentorship_eligibility.csv)

---

### The Number of Retiring Employees by Title   
**Retirement Titles Table**    
            1. retrieve `emp_no`, `first_name`, and `last_name` columns from employees table    
            2. retrieve `title`, `from_date`, and `to_date` columns from titles table   
            3. create new table called retirement_titles using `INTO` clause    
            4. join the Employees and Titles tables on primary key (`emp_no`)    
            5. filter data on `birth_date column` to retrieve employees born between 1952 & 1955 (order results by `emp_no`)    
            6. `DISTINCT ON` statement to retrieve most recent title of each employee   
            7. insert results into retirement_titles table   
            8. count number of retirement-age employees by most recent job title   
            9. order results by count in descending order   
            10. export retirement_titles table as a CSV file [retirement_titles.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/retirement_titles.csv)
  
**Unique Titles Table**      
            1. retrieve ***employee number***, ***first*** and ***last name***, and ***title*** columns from the **Retirement Titles table**    
            2. use the `DISTINCT ON` statement to retrieve the first occurrence of employee number for each set of rows defined by the `ON ()` clause    
            3. excludes those employees that have already left the company by filtering on `to_date` to keep only those dates that are equal to `'9999-01-01'`    
            4. creates **Unique Titles table** using `INTO` clause   
            5. sorts **Unique Titles table** by   
                        - *ascending* order by ***employee number*** of most recent title    
                        - *descending* order by ***last date*** (e.g., `to_date`) of most recent title    
            6. The Unique Titles table is exported as [unique_titles.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/unique_titles.csv)  

**Retiring Titles Table**     
            1. retrieve ***titles*** and uses `COUNT()` to retrieve the ***number of titles*** from the **Unique Titles table**     
            2. create **Retiring Titles table** to hold required information of ***number of titles filled by employees who are retiring     
            3. group table by ***title***, then sort the count column in *descending* order     
            4. export The Ritiring Titles table as [retiring_titles.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/retiring_titles.csv)     

---

### The Employees Elegibile for the Mentorship Program

**Mentorship Eligibility Table**    
            1. retrieve the `emp_no`, `first_name`, `last_name`, and `birth_date` columns from the Employees table     
            2. retrieve the `from_date` and `to_date` columns from the Department Employee table      
            3. retrieve the `title` column from the Titles table      
            4. use a `DISTINCT ON` statement to retrieve the first occurrence of the employee number for each set of rows defined by the `ON ()` clause     
            5. create a new table using the `INTO` clause      
            6. join the Employees and the Department Employee tables on the primary key     
            7. join the Employees and the Titles tables on the primary key     
            8. filter the data on the `to_date column` to all the current employees, then filter the data on the `birth_date` columns to get all the employees whose birth dates are between January 1, 1965 and December 31, 1965    
            9. order the table by the employee number    
            10. export the Mentorship Eligibility table as [mentorship_eligibilty.csv](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/data/mentorship_eligibility.csv)    

---
---

## Results
From the four tables generated from the Pewlett Hackard's employee database, it can be inferred:  
- there are 133,776 job title positions within Pewlett Hackard eligible to retire *as shown by the retirement_titles table below:*
![retirement_titles](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/images/retirement_titles.png)  
- there are 72,458 employees within the company eligible to currently retire *as shown by the unique_titles table below:*
![unique_titles](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/images/unique_titles.png)
- the majority of employees retiring are Senior Engineers and Senior Staff *as shown by the retiring_titles table below:*
![retiring_titles](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/images/retiring_titles.png)  
- 1,549 employees are currently eligible for mentorship opportunities to take over retiring employees *as shown by the total row count in the mentorship_eligibilitiy table below:*  
![mentorship_eligibility](https://github.com/vzhang90/Pewlett-Hackard-Analysis/blob/main/images/mentorship_eligibility.png)  

## Summary
72,458 roles will need to be filled at Pewlett Hackard as the "silver tsunami" begins to make an impact.

With only 1,549 employees eligible for mentorship opportunities to take over retiring employees, there is definitely enough qualified, retirement-ready employees (72,458) in the departments to mentor the next generation of Pewlett Hackard employees.

For future investigations that may provide more insight into the upcoming "silver tsunami", it could be even more insightful to another query to generate a Salaries table to forecast the payroll funds after this labor shift. 

It would also be helpful to create a query to reflect the upcoming departures of the many employees retiring in the management team. The result of this query would show only 5 departments have active managers while the retiring_titles table shows 2 retiring managers, meaning potentially 7 upcoming manager positions needed at Pewlett Hackard.
