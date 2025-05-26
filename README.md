SQL Project        =  ScienceQtech-Employee-Performance-Mapping


Author             =  Deepika Rani

Problem scenario
------------------

ScienceQtech is a startup that works in the Data Science field. ScienceQtech has worked on fraud detection, market basket, self-driving cars, supply chain, algorithmic early detection of lung cancer, customer sentiment, and the drug discovery field. With the annual appraisal cycle around the corner, the HR department has asked you (Junior Database Administrator) to generate reports on employee details, their performance, and on the project that the employees have undertaken, to analyze the employee database and extract specific data based on different requirements.


Objective
-----------

To facilitate a better understanding, managers have provided ratings for each employee which will help the HR department to finalize the employee performance mapping. As a DBA, you should find the maximum salary of the employees and ensure that all jobs are meeting the organization's profile standard. You also need to calculate bonuses to find extra cost for expenses. This will raise the overall performance of the organization by ensuring that all required employees receive training.


Dataset description
------------------------

emp_record_table: It contains the information of all the employees.

                          ●	EMP_ID – ID of the employee
  
                          ●	FIRST_NAME – First name of the employee

                          ●	LAST_NAME – Last name of the employee

                          ●	GENDER – Gender of the employee

                          ●	ROLE – Post of the employee

                          ●	DEPT – Field of the employee

                          ●	EXP – Years of experience the employee has

                          ●	COUNTRY – Country in which the employee is presently living

                          ●	CONTINENT – Continent in which the country is

                          ●	SALARY – Salary of the employee

                          ●	EMP_RATING – Performance rating of the employee

                          ●	MANAGER_ID – The manager under which the employee is assigned
  
                          ●	PROJ_ID – The project on which the employee is working or has worked on


Proj_table: It contains information about the projects.

                          ●	PROJECT_ID – ID for the project

                          ●	PROJ_Name – Name of the project
    
                          ●	DOMAIN – Field of the project

                          ●	START_DATE – Day the project began

                          ●	CLOSURE_DATE – Day the project was or will be completed

                          ●	DEV_QTR – Quarter in which the project was scheduled

                          ●	STATUS – Status of the project currently

Data_science_team: It contains information about all the employees in the Data Science team.

                          ●	EMP_ID – ID of the employee
                          
                          ●	FIRST_NAME – First name of the employee

                          ●	LAST_NAME – Last name of the employee

                          ●	GENDER – Gender of the employee

                          ●	ROLE – Post of the employee

                          ●	DEPT – Field of the employee

                          ●	EXP – Years of experience the employee has

                          ●	COUNTRY – Country in which the employee is presently living
  
                          ●	CONTINENT – Continent in which the country is




The Tasks to be performed
---------------------------


1. Create a database named employee, then import data_science_team.csv proj_table.csv and emp_record_table.csv into the employee database from the given resources.

Query:
      
      Create Database employee;

Output :

![image](https://github.com/user-attachments/assets/c4538cfd-8f3c-46de-b54c-179c6883c7f8)

2. Create an ER diagram for the given employee database.

Output:

![image](https://github.com/user-attachments/assets/0bf20c8d-c20b-486f-b570-ee50bc1fffe8)


3. Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.

Query:

          use employee;

          SELECT  EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT 'Department'

          FROM emp_record_table;


Output :

![image](https://github.com/user-attachments/assets/2cb300ff-0555-4936-848e-9285536bc03b)


4. Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is: 

●	less than two

●	greater than four 

●	between two and four

Query:

          use employee;
          SELECT  EMP_ID, FIRST_NAME,	 LAST_NAME, GENDER, DEPT 'Department', EMP_RATING

          FROM emp_record_table

          WHERE  EMP_RATING < 2 OR EMP_RATING > 4
       
          OR (EMP_RATING >= 2 AND EMP_RATING <= 4);

Output :

![image](https://github.com/user-attachments/assets/9be4f607-f2fd-4a85-89f4-38ca0c6c1aa7)


5. Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.


Query:

        use employee;

        SELECT  EMP_ID, CONCAT(FIRST_NAME, ' ', LAST_NAME) 'Name', DEPT 'Department'

        FROM emp_record_table

        WHERE DEPT = 'FINANCE';

Output : 

![image](https://github.com/user-attachments/assets/35d08f92-65a4-4fa5-9f44-40c31eea5176)


6. Write a query to list only those employees who have someone reporting to them. Also, show the number of reporters (including the President).

Query:

        use employee;

        SELECT  m.EMP_ID, m.FIRST_NAME,  m.LAST_NAME, COUNT(r.EMP_ID) 'Number_of_Reporters'

        FROM  emp_record_table m
        
        JOIN
    
        emp_record_table r ON m.EMP_ID = r.MANAGER_ID

        GROUP BY 1 , 2 , 3;

# m - represents employees who report to the manager

# r - represents number of reporters


Output : 

![image](https://github.com/user-attachments/assets/d89230cd-fd25-4351-baf3-569bed3f685e)


7. Write a query to list down all the employees from the healthcare and finance departments using union. Take data from the employee record table.

Query:

        SELECT  * FROM
   
        emp_record_table

        WHERE DEPT = 'HEALTHCARE' 

        UNION SELECT * FROM emp_record_table

        WHERE  DEPT = 'FINANCE';

Output :

![image](https://github.com/user-attachments/assets/9f4df784-9a93-4fc1-97f1-e19c051751da)


8. Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective employee rating along with the max emp rating for the department.

Query:

        SELECT e.EMP_ID, e.FIRST_NAME, e.LAST_NAME, e.ROLE, e.DEPT,  e.EMP_RATING, d.Max_EMP_RATING_dept

        FROM  emp_record_table e
        
        JOIN
   
        (SELECT  DEPT, MAX(EMP_RATING) Max_Emp_Rating_Dept
   
        FROM emp_record_table d
    
        GROUP BY DEPT) d ON e.DEPT = d.DEPT;

Output :

![image](https://github.com/user-attachments/assets/172b30ea-c1dc-4d16-a222-826cacec5897)


9. Write a query to calculate the minimum and the maximum salary of the employees in each role. Take data from the employee record table.

Query:

        SELECT ROLE, MIN(SALARY) 'Min_Salary', MAX(SALARY) 'Max_Salary'

        FROM  emp_record_table

        GROUP BY ROLE;

Output :

![image](https://github.com/user-attachments/assets/619386e2-e0b9-441b-8bbd-bc98e9e7a847)


10. Write a query to assign ranks to each employee based on their experience. Take data from the employee record table.

Query:

        SELECT EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPT, EXP,
        Dense_RANK () OVER (ORDER BY EXP DESC) 'Exp_Rank'
        FROM emp_record_table;


Output :

![image](https://github.com/user-attachments/assets/65ab07bb-465b-4a8d-a3db-2f1bfc054aa1)


11. Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.

Query:

      CREATE VIEW High_Salary_Employees AS
     
      SELECT *
      
      FROM emp_record_table

      WHERE SALARY > 6000;

      SELECT * FROM High_Salary_Employees;

Output :

![image](https://github.com/user-attachments/assets/23990187-6600-4e2d-a957-a5d84decfdad)


12. Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.

Query:

      SELECT  * FROM emp_record_table

      WHERE EMP_ID IN (SELECT EMP_ID
        
      FROM emp_record_table
        
      WHERE EXP > 10);

Output:

![image](https://github.com/user-attachments/assets/68bfd49b-5ae5-46a3-b6ab-75a0e53bf613)


13. Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three years. Take data from the employee record table.

Query:

        Delimiter //

        CREATE  PROCEDURE get_experienced_employees()
        BEGIN

        SELECT * FROM emp_record_table
        WHERE EXP > 3;
        END //
        Delimiter ;
        call  get_experienced_employees();


Output :

![image](https://github.com/user-attachments/assets/e00b8cd9-87e6-4c51-af6c-1d3aaf6d4cd5)


14. Write a query using stored functions in the project table to check whether the job profile assigned to each employee in the data science team matches the organization’s set standard.

    The standard being:
    
    For an employee with experience less than or equal to 2 years assign 'JUNIOR DATA SCIENTIST',

    For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA SCIENTIST',

    For an employee with the experience of 5 to 10 years assign 'SENIOR DATA SCIENTIST',

    For an employee with the experience of 10 to 12 years assign 'LEAD DATA SCIENTIST',
  
    For an employee with the experience of 12 to 16 years assign 'MANAGER'.\

Query:

    DELIMITER //

    CREATE FUNCTION Check_Standard_Profile(emp_exp INT, emp_role VARCHAR(50))

    RETURNS VARCHAR(20)

    DETERMINISTIC

    BEGIN
    
    DECLARE standard_role VARCHAR(50);

    IF emp_exp <= 2 THEN
        
        SET standard_role = 'JUNIOR DATA SCIENTIST';
   
    ELSEIF emp_exp > 2 AND emp_exp <= 5 THEN
        
        SET standard_role = 'ASSOCIATE DATA SCIENTIST';
    
    ELSEIF emp_exp > 5 AND emp_exp <= 10 THEN
       
        SET standard_role = 'SENIOR DATA SCIENTIST';
    
    ELSEIF emp_exp > 10 AND emp_exp <= 12 THEN
        
        SET standard_role = 'LEAD DATA SCIENTIST';
    
    ELSEIF emp_exp > 12 AND emp_exp <= 16 THEN
        
        SET standard_role = 'MANAGER';

    ELSE
       
        SET standard_role = 'UNKNOWN';
    
    END IF;

    RETURN IF(emp_role = standard_role, 'Match', 'No Match');
    END //
    DELIMITER ;
    SELECT EMP_ID, FIRST_NAME, LAST_NAME, ROLE, EXP,
    Check_Standard_Profile(EXP, ROLE) AS Profile_Match_Status
    FROM  data_science_team;

Output:

![image](https://github.com/user-attachments/assets/e0ac16fb-37c2-47c0-9a3a-38895e7501d3)


15. Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.

Query:

        use employee;

        EXPLAIN SELECT * FROM emp_record_table WHERE FIRST_NAME = 'Eric';

        SHOW SESSION STATUS LIKE 'Handler_read%';

        SELECT * FROM emp_record_table WHERE FIRST_NAME = 'Eric';

        CREATE INDEX idx_first_name ON emp_record_table(FIRST_NAME(20));

        EXPLAIN SELECT * FROM emp_record_table WHERE FIRST_NAME = 'Eric';

        SHOW SESSION STATUS LIKE 'Handler_read%';


Output:

![image](https://github.com/user-attachments/assets/8972a012-ef75-411e-9ab8-22140f6cbfd1)


16. Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating).

Query:

      SELECT  EMP_ID, FIRST_NAME, SALARY, EMP_RATING,
    
      (0.5 * SALARY * EMP_RATING) 'Bonus'

      FROM  emp_record_table;

  

Output:

![image](https://github.com/user-attachments/assets/1e3374da-2834-4b24-a0c8-622a1fed59fd)


17. Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.

Query:

      SELECT CONTINENT, COUNTRY, AVG(SALARY) 'Average_Salary'

      FROM emp_record_table

      GROUP BY CONTINENT , COUNTRY;



Output:

![image](https://github.com/user-attachments/assets/62d0ddad-a45b-4b65-8603-6b71088ab6f2)
