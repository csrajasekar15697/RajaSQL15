# RajaSQLBipp

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

