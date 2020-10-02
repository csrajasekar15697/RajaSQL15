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
Consider P1 and P2 to be two points on a 2D plane.

 a happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
 b happens to equal the minimum value in Western Longitude (LONG_W in STATION).
 c happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
 d happens to equal the maximum value in Western Longitude (LONG_W in STATION).
Query the Manhattan Distance between points P1(a,b) and P2(c,d) and round it to a scale of 4 decimal places.


Answer:

SELECT ABS(ROUND((MIN(LAT_N)-MAX(LAT_N))+(MIN(LONG_W)-MAX(LONG_W)),4))
FROM STATION;

2)



