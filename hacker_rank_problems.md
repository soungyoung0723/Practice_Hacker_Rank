## Basic-select
### SELECT by ID

###
Query all columns for a city in CITY with the ID 1661.

Input Format

The CITY table is described as follows: 

![Image](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg) 


-- Solution

SELECT *   

FROM city     

WHERE ID = 1661;

###
Query the names of all the Japanese cities in the CITY table. 

The COUNTRYCODE for Japan is JPN.

Input Format

The CITY table is described as follows:

![Image](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)


-- Solution

SELECT name

FROM city

WHERE countrycode = 'JPN';

###
Let  be the number of CITY entries in STATION, and let  be the number of distinct CITY names in STATION; query the value of  from STATION. In other words, find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

Input Format

The STATION table is described as follows:

-----STATION-----

Field     Type

ID        NUMBER

CITY      VARCHAR2(21)

STATE     VARCHAR2(2)

LAT_N     NUMBER

LONG_W    NUMBER  

where LAT_N is the northern latitude and LONG_W is the western longitude.


-- Solution

SELECT COUNT(CITY) - COUNT(DISTINCT CITY) AS N 

FROM STATION; 

###

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
Input Format
The STATION table is described as follows:

-----STATION-----

Field     Type

ID        NUMBER

CITY      VARCHAR2(21)

STATE     VARCHAR2(2)

LAT_N     NUMBER

LONG_W    NUMBER  


where LAT_N is the northern latitude and LONG_W is the western longitude.


Sample Input

Let's say that CITY only has four entries: DEF, ABC, PQRS and WXY

Sample Output

ABC 3

PQRS 4


Explanation

When ordered alphabetically, the CITY names are listed as ABC, DEF, PQRS, and WXY, with 
the respective lengths 3,3,4 and 3. The longest-named city is obviously PQRS, but there 
are 3 options for shortest-named city; we choose ABC, because it comes first alphabetically.


Note

You can write two separate queries to get the desired output. 
It need not be a single query.

-- Solution

SELECT min(city), city_len

FROM ( SELECT city, length(city) city_len,

      max(length(city)) over() maxlen, 

      min(length (city)) over() minlen 

      FROM station)

WHERE city_len in(minlen, maxlen)

GROUP BY city_len;

###
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) 
from STATION. Your result cannot contain duplicates.


Input Format

The STATION table is described as follows:


-----STATION-----

Field     Type  

ID        NUMBER

CITY      VARCHAR2(21)

STATE     VARCHAR2(2)

LAT_N     NUMBER

LONG_W    NUMBER  



-- Solution

SELECT DISTINCT city FROM   station

WHERE  city  LIKE 'A%' 

or  city  LIKE 'E%' 

or city  LIKE 'I%'

or city  LIKE 'O%' 

or city  LIKE 'U%';

--- convert


Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION.


SELECT DISTINCT city FROM   station

WHERE  city  LIKE '%a' 

or  city  LIKE '%e' 

or city  LIKE '%i'

or city  LIKE '%o' 

or city  LIKE '%u';