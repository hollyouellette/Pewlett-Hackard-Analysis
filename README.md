# Pewlett Hackard Analysis

## Overview of the Analysis

The purpose of this analysis was to support the Pewlett Hackard organization in organizing and anlyzing employee data preceding thousands of their employees reaching retirement age. To plan for this "silver tsunami", Pewlett Hackard is scrubbing through all of their employee data to identify both the employees who will be offered retirement packages as well as the employess nearing retirement age. The employees who are within 10 years of retirement are eligibile for a Mentorship Program to support with the turnover of thousands of employees in new roles. The following analysis used SQL to query the existing Database containing employee information dating back as far as these records have been kept for Pewlett Hackard. Based on the employe data, this analysis provides two new csv. files; one detailing the number of retiring employees by title and the other identifying employees eligible for the Mentorship Program based on their birth year. 

## Results

The analaysis of Pewlett Hackard's employee data yielded the following four major results:

- The retiring_titles.csv showcases that Packard Hewlett has 78,155 employees nearling retirement age. The vast majority of these employeess are in a **Senior, Leader** or **Manager Role**, representint 62,173 of total number of employees reaching retirement age. 
- 74% of Pewlett Hackard's employees reaching retirement age are either Senior Engineers or Senior Staff.
- The mentorship_eligibility.csv indicates that there are 402 Senior Engineers and 281 Senior Staff that can support in the Mentorship Program, which will be crutial knowing that these two Job Titles make up nearly 3/4 of as positions that will require filling due to the "silver tsunami".
- Based on this analysis, there are no Managers meet eligibility for the Mentorship Program.

## Summary

#### How many roles will need to be filled as the "silver tsunami" begins to make an impact?

   As the "silver tsunami" begins to make an impact, a total of 78,155 roles will need to be filled.

#### Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
   Yes and no. For the majority of the deparments, there are enough qulified, retirement-ready employees to be a part of the Mentorshop Program. They will be especially set up for success because the Senir Engineer and Senior Sales titles each have hundreds of employees who are qualified to mentor the several thousand new employees that will require mentorship in their departments. Pewlett Hackard should be concerned, however, that there are no Managers who qualify for the Mentorshop Program. This is potential roadblock is addressed in the additional queries below.

#### Additional Queries

In addition to the analysis that was performed in this assignment, additional queries could be used to help Pewlett Hackard plan for the upcoming "silver tsunami" in a couple of ways.

**First**, I would recommend builing a query to widen the age parameters of the Mentorship Program eligibility for the Manager title specifically. With two upcoming retirements and no eligible employees to build the Manager pipeline as mentors, it would be wise to adjust the parameters to ensure that there is strong future-planning in place for this role. 

<img src="https://github.com/hollyouellette/Pewlett-Hackard-Analysis/blob/main/future_metorship_manager_query.png" width=200 align=left>

With this query, we are able to include employees with birthdays extending forward 5 additional years for the manager title specifically. By performing this, Pewlett Hackard's mentorship program would include 10 potential mentors to build their Manager pipeline and successfully future-proof this department.

<img src="https://github.com/hollyouellette/Pewlett-Hackard-Analysis/blob/main/future_mentoryship_eligibility.png">
<br/><br/<br/>
<img src="https://github.com/hollyouellette/Pewlett-Hackard-Analysis/blob/main/unique_upcoming_retirement.png" align=right width=300>**Second**, I would recommend building out a strategy to address the upcoming retirements and subsequent role vacancies over the next 10 years. This could be accomplished by using a query to: 
     - Isolate the employees who were born between 1956 to 1966 and sorting them by title and birthday.
     - Next, to ensure that each imployee is counted only once, setting the query to be distinct on the employee number
     - Producing an employee count by title to visualize how many employees each department should be planning to replace due to retirement over the next 10 years. 
     
    
<img src="https://github.com/hollyouellette/Pewlett-Hackard-Analysis/blob/main/next_ten_yrs_query.png">
     
    SELECT DISTINCT ON (e.emp_no) e.emp_no, e.first_name, e.last_name, e.birth_date,
            de.from_date, de.to_date, t.title
        INTO future_mentorship_eligibility
        FROM employees as e
        JOIN dept_emp as de
          ON (e.emp_no=de.emp_no)
        JOIN titles as t
         ON (t.emp_no=e.emp_no)
        WHERE (de.to_date='9999-01-01')
          AND e.birth_date BETWEEN '1960-01-01' AND '1965-12-31'
          AND (t.title='Manager')
        ORDER BY e.emp_no;

Upcoming Retirement for the next 10 years to create a strong pipeline plan
