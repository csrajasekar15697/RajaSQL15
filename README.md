# RajaSQL15

Easy Category 

1) Query a list of CITY and STATE from the STATION table?

Answer:

SELECT CITY,STATE 
FROM STATION;

2)Query the average population for all cities in CITY, rounded down to the nearest integer?
 
Answer:

SELECT ROUND(AVG(POPULATION))
FROM CITY;

3)Query a count of the number of cities in CITY having a Population larger than 100000?

Answer:

SELECT COUNT(NAME)
FROM CITY
WHERE POPULATION > 100000;

4)Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.

Answer:

SELECT * FROM CITY
WHERE COUNTRYCODE = 'JPN';

5)Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

Equilateral: It's a triangle with  sides of equal length.
Isosceles: It's a triangle with  sides of equal length.
Scalene: It's a triangle with  sides of differing lengths.
Not A Triangle: The given values of A, B, and C don't form a triangle.

Answer:

SELECT CASE 
WHEN A+B>C 
    THEN CASE 
    WHEN A=B AND B=C THEN 'Equilateral'
    WHEN A=B OR B=C OR A=C THEN 'Isosceles'
    WHEN A!=B OR B!=C OR A!=C THEN 'Scalene'
    END ELSE 'Not A Triangle' END FROM TRIANGLES;

6)Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

Answer:

SELECT SUM(CITY.POPULATION)
FROM CITY,COUNTRY 
WHERE CITY.COUNTRYCODE = COUNTRY.CODE
AND CONTINENT = 'Asia';

Medium Category 

1)
Consider P1 and P2 to be two points on a 2D plane.

 a happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
 b happens to equal the minimum value in Western Longitude (LONG_W in STATION).
 c happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
 d happens to equal the maximum value in Western Longitude (LONG_W in STATION).
Query the Manhattan Distance between points P1(a,b) and P2(c,d) and round it to a scale of 4 decimal places.


Answer:

SELECT ABS(ROUND((MIN(LAT_N)-MAX(LAT_N))+(MIN(LONG_W)-MAX(LONG_W)),4))
FROM STATION;

2)Generate the following two result sets:

Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:

There are a total of [occupation_count] [occupation]s.
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

Answer:

SELECT (Name || '(' || UPPER(SUBSTR(Occupation,1,1)) || ')') AS NAME FROM OCCUPATIONS
ORDER BY NAME;

SELECT 'There are a total of ' || COUNT(Name) || ' ' ||LOWER(Occupation) || 's.' FROM OCCUPATIONS GROUP BY Occupation
ORDER BY Count(Name),Occupation;

3) Consider P1(a,c) and P1(b,d) to be two points on a 2D plane where (a,b) are the respective minimum and maximum values of Northern Latitude (LAT_N) and (c,d) are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.

Query the Euclidean Distance between points P1 and P2  and format your answer to display  decimal digits.

ANSWER :

SELECT ROUND(SQRT(POWER(MAX(LAT_N)-MIN(LAT_N),2)+POWER(MAX(LONG_W)-MIN(LONG_W),2)),4)
FROM STATION;

4)Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

Write a query to help Eve.

Answer :

UPDATE Students
SET Name = 'NULL'
WHERE Marks < 70;

SELECT Students.Name,Grades.Grade,Students.Marks
FROM Students,Grades
WHERE (Students.Marks BETWEEN Grades.Min_Mark AND Grades.MAX_MARK)
ORDER BY Grades.Grade DESC,Students.Name ASC;

5)You are given three tables: Students, Friends and Packages. Students contains two columns: ID and Name. Friends contains two columns: ID and Friend_ID (ID of the ONLY best friend). Packages contains two columns: ID and Salary (offered salary in $ thousands per month).



Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.

Answer:

SELECT temp1.sn
FROM (SELECT S.ID si,S.Name sn,P.Salary ps FROM Students S JOIN Packages P on S.ID=P.ID) temp1 JOIN (SELECT FF.ID fi,FF.Friend_ID fd,PP.Salary pps FROM Friends FF JOIN Packages PP on FF.Friend_ID=pp.ID) temp2 ON temp1.si=temp2.fi AND temp1.ps<temp2.pps
ORDER BY temp2.pps ASC;

6)Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.

Note:

The tables may contain duplicate records.
The company_code is string, so the sorting should not be numeric. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.

Answer:


SELECT C.Company_Code, C.founder, COUNT(Distinct E.Lead_Manager_Code), 
COUNT(distinct E.Senior_Manager_Code), COUNT(distinct E.Manager_Code), 
COUNT(distinct E.employee_Code) 
FROM Company C 
JOIN Employee E 
ON C.Company_Code = E.Company_Code 
GROUP BY C.Company_Code, C.Founder 
ORDER BY C.Company_Code;
