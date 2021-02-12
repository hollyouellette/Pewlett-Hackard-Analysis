# Pewlett Hackard Analysis

## Overview of the Analysis

The purpose of this analysis was to support the Pewlett Hackard organization in organizing and anlyzing employee data in the wake of thousands of their employees reaching retirement age. Pewlett Hackard is looking to address this in two ways: first, by offering retirement packages for those who meet eligibility requirements and second, transitioning employees nearing retirement into a Part Time Mentorship program to support with the turnover of thousands of employees in new roles. This analysis used SQL to Query the existing Database containing employee information dating back to when the company was orignally created. Based on the employe data, this analysis provides a csv. file detailing the number of retiring employees by title as well as employees eligible for the Mentorship Program.

## Results

- Packard Hewlett has 78155 employees nearling retirement age, 62173 of which are in a Senior, Leader or Manager role.
- 74% of employees reaching retirement age are either Senior Engineers or Senior Staff
- 402 Senior Engineers and 281 Senior Staff that can support in the Mentorship Program as these new positions are filled
- No Managers meet eligibility for the Mentorship Program

## Summary
- 78155 roles will need to be filled
- very strategic with SE and SS because though they have many mentors, they are filling the most roles
- this could be an issue with the manager program

Additional Query - Planning Ahead for Manager Mentors
     
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
