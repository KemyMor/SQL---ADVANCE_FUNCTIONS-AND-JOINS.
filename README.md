# SQL---ADVANCE_FUNCTIONS-AND-JOINS.
**Skills used: Joins, Temp Tables, String Functions, Aggregate Functions, Creating Views, Converting Data Types**

## Showing the total yearly salaries of employees across all designation. Showing only designation with and order the results by department name.
*Note: -- If the data type of the column is nvarchar, you can convert it to a numeric type in the SUM function
SELECT SUM(CONVERT(DECIMAL(18, 2), REPLACE(REPLACE(Columu_name, '$', ''), ',', ''))) FROM Table_name;*

---SELECT 
    name, 
    Designation, 
    SUM(CONVERT(DECIMAL(18, 2), REPLACE(REPLACE(Base, '$', ''), ',', ''))) AS TOTAL_EARNINGS
FROM 
    Employee 
INNER JOIN 
    Department ON Employee.DeptID = Department.DeptID
INNER JOIN 
    Salary ON Employee.empID = Salary.empID
GROUP BY 
    name, Designation
ORDER BY    
    Designation;
----
![Employees_TotalYearlyIncrement](https://github.com/KemyMor/SQL---ADVANCE_FUNCTIONS-AND-JOINS./blob/a006d035ffd3c52c977b2777dc3de83a9988a260/Employees_TotalYearlyIncrement.png)
*Cross-section of employee's total yealy salary.* 

## Showing the names of all employees along with their department names. Include employees with no assigned department, and sort the result by employee name.

----SELECT name, Designation
    FROM Employee
    JOIN Department ON Employee.DeptID = Department.DeptID
    GROUP BY name, Designation
    ORDER BY name ;
------
![Employees_Designation](https://github.com/KemyMor/SQL---ADVANCE_FUNCTIONS-AND-JOINS./blob/a006d035ffd3c52c977b2777dc3de83a9988a260/Employees_Designation.jpg)
*Cross-section of Employee's and their designation.*

## Showing the average yearly increment for employees in each department.

----SELECT 
        CONCAT(Employee.name, ' ', Employee.fname) AS Full_Name, 
        Department.Designation, 
        AVG(Salary.[yearly increment]) AS AvgYearlyIncrement
    FROM 
        Employee 
    JOIN 
        Salary ON Employee.empID = Salary.empID
    JOIN 
        Department ON Employee.DeptID = Department.DeptID
    GROUP BY 
        CONCAT(Employee.name, ' ', Employee.fname), Department.Designation
    ORDER BY 
        Full_Name;
------
![Employees_AvgYearlyIncrement](https://github.com/KemyMor/SQL---ADVANCE_FUNCTIONS-AND-JOINS./blob/a006d035ffd3c52c977b2777dc3de83a9988a260/Employees_AvgYearlyIncrement.jpg)
*Cross-section of employee's average yearly increment.*

## Showing the average yearly increment for employees in each department. Showing departments with an average yearly increment greater than 5000 only.

----- SELECT
            Employee.name, Department.Designation, 
            AVG(Salary.[yearly increment]) AS AvgYearlyIncrement
      FROM Employee 
      JOIN Salary ON Employee.empID = Salary.empID
      JOIN Department ON Employee.DeptID = Department.DeptID
      GROUP BY Department.Designation, Employee.name
      HAVING AVG(Salary.[yearly increment]) > 5000
      ORDER BY Employee.name;
-------
![Employees_AvgIncrement_Above5000](https://github.com/KemyMor/SQL---ADVANCE_FUNCTIONS-AND-JOINS./blob/a006d035ffd3c52c977b2777dc3de83a9988a260/Employees_AvgIncrement_Above5000.jpg)
*Employees average yearly increment greater than 5000*


