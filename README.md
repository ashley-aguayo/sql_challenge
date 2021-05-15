# sql_challenge
-- list employees plus salary
 SELECT e.emp_no,
    e.last_name,
    e.first_name,
    e.sex,
    s.salary
   FROM employees e
     JOIN salaries s ON e.emp_no = s.emp_no;

--employees hired in 1986
select first_name,last_name,hire_date
from employees
where hire_date between '1986-01-01' and '1986-12-31';

create view hired_1986
as
select first_name,last_name,hire_date
from employees
where hire_date between '1986-01-01' and '1986-12-31';

--List the manager of each department with the following information: department number, department name, 
--the manager's employee number, last name, first name.
create view dept_mgr_details
as
Select dmv.dept_no,
		dmv.emp_no,
		dmv.last_name,
		dmv.first_name,
		d.dept_name
FROM dept_mgr_3 as dmv
INNER JOIN deparments as d
	on dmv.dept_no=d.dept_no;

-- List the department of each employee with the following information: employee number, last name, first name,
-- and department name.

Select * from dept_emp;

create view emp_de
as
Select e.emp_no,
		e.last_name,
		e.first_name,
		de.dept_no
from employees as e
inner join dept_emp as de 
	on e.emp_no=de.emp_no
Create view emp_w_dept
as
Select e.emp_no,
		e.last_name,
		e.first_name,
		e.dept_no,
		d.dept_name
from emp_de as e
inner join deparments as d
	on e.dept_no=d.dept_no


---List first name, last name, and sex for employees whose first name is "Hercules" and last names begin with "B."
Create View emp_hercules
as
SELECT first_name,
		last_name,
		sex
FROM employees
WHERE first_name = 'Hercules'
AND last_name like 'B%';

--List all employees in the Sales department, including their employee number, 
--last name, first name, and department name.
select * from deparments;

--sales d007
select * from emp_w_dept;
Select emp_no,
		first_name,
		last_name,
		dept_name
FROM emp_w_dept
WHERE dept_no = 'd007';
		
--List all employees in the Sales and Development departments, including their employee number,
--last name, first name, and department name.
select * from emp_w_dept;
Select emp_no,
		first_name,
		last_name,
		dept_name
FROM emp_w_dept
WHERE 
	dept_no = 'd007'
	or dept_no = 'd005';
	
--In descending order, list the frequency count of employee last names, i.e., how many employees share each last name.
SELECT COUNT(last_name) AS "Last Name Count"
FROM employees
GROUP BY last_name
ORDER BY last_name DESC;

