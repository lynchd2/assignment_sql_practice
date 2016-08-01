AUTHORS: DYLAN, ADRIAN
====== 

SQLZoo
------



### Select Basics 

* Modify it to show the population of Germany

```sql
  SELECT population 
  FROM world
  WHERE name = 'Germany'

```

* Show the name and the population for 'Ireland', 'Iceland' and 'Denmark'.


```sql

  SELECT name, population 
  FROM world
  WHERE name IN ('Ireland', 'Iceland', 'Denmark');

```

* Just the right size


```sql

  SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000

```

### Select from World

+ Observe the result of running a simple SQL command.

```sql

  SELECT name, continent, population 
  FROM world

```

+ Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

```sql

  SELECT name, continent, population 
  FROM world

```

+ Give the name and the per capita GDP for those countries with a population of at least 200 million.

```sql


SELECT name, gdp / population as per_capita
FROM world
WHERE population > 200000000


```

+ Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

```sql

SELECT name, population as pop_in_millions
FROM world
WHERE continent = 'South America'

```

+ Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.


```sql

SELECT name, population as pop_in_millions
FROM world
WHERE continent = 'South America'

```

+ Show the name and population for France, Germany, Italy

```sql

SELECT name, population FROM world
WHERE name IN ('France', 'Germany', 'Italy')

```

+ Show the countries which have a name that includes the word 'United'

```sql

SELECT name FROM world
WHERE name LIKE '%United%'

```

+ Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.

Show the countries that are big by area or big by population. Show name, population and area.

```sql

SELECT name, population, area FROM world
WHERE population > 250000000 OR area > 3000000

```

+ Exclusive OR (XOR). Show the countries that are big by area or big by population but not both. Show name, population and area.

Australia has a big area but a small population, it should be included.
Indonesia has a big population but a small area, it should be included.
China has a big population and big area, it should be excluded.
United Kingdom has a small population and a small area, it should be excluded.

```sql
SELECT name, population, area FROM world
WHERE population > 250000000 XOR area > 3000000

```

+ Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.

For South America show population in millions and GDP in billions both to 2 decimal places.

```sql
SELECT name,
    ROUND(population/1000000, 2), 
    ROUND(gdp/1000000000, 2)
  FROM world
WHERE continent = 'South America'
```

+ Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

Show per-capita GDP for the trillion dollar countries to the nearest $1000.

```sql
SELECT name, ROUND(gdp/population, -3) FROM world
WHERE gdp >= 1000000000000`
```

```sql
SELECT name, ROUND(gdp/population, -3) FROM world
WHERE gdp >= 1000000000000`
```

+ The CASE statement shown is used to substitute North America for Caribbean in the third column.

```sql

Show the name - but substitute Australasia for Oceania - for countries beginning with N.
    SELECT name,
    CASE WHEN continent = 'Oceania' THEN 'Australasia'
            ELSE continent END
    FROM world
    WHERE name LIKE 'N%'

```

Put the continents right...

Oceania becomes Australasia
Countries in Eurasia and Turkey go to Europe/Asia
Caribbean islands starting with 'B' go to North America, other Caribbean islands go to South America
Order by country name in ascending order
Show the name, the original continent and the new continent of all countries.

```sql

  SELECT name, 
       CASE WHEN continent = 'Europe' THEN 'Eurasia'
            WHEN continent = 'Asia' THEN 'Eurasia'
            WHEN continent = 'North America' THEN 'America'
            WHEN continent = 'South America' THEN 'America'
            WHEN continent = 'Caribbean' THEN 'America'
            ELSE continent END
            FROM world
  WHERE name LIKE 'A%' OR name LIKE 'B%'
```

### SELECT from Nobel

+ Change the query shown so that it displays Nobel prizes for 1950.


```sql

  SELECT yr, subject, winner
  FROM nobel
  WHERE yr = 1950

```

+ Show who won the 1962 prize for Literature.

```sql

  SELECT winner
  FROM nobel
  WHERE yr = 1962
    AND subject = 'Literature'

```

+ Show the year and subject that won 'Albert Einstein' his prize.

```sql
  SELECT yr, subject
  FROM nobel
  WHERE winner = 'Albert Einstein'

```
+ Give the name of the 'Peace' winners since the year 2000, including 2000.


```sql
  SELECT winner
  FROM nobel
  WHERE yr > 1999 AND subject = 'Peace'

```

+ Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive.

```sql
  SELECT yr, subject, winner 
  FROM nobel
  WHERE yr >= 1980 AND yr <= 1989 AND subject = 'Literature'
```

+ Show all details of the presidential winners:

```sql
	SELECT * 
	FROM nobel
	WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter')
```

+ Show the winners with first name John

```sql
	SELECT winner
	FROM nobel
	WHERE winner LIKE 'John%'
```

+ Show the Physics winners for 1980 together with the Chemistry winners for 1984.

```sql
	SELECT *
	FROM nobel
	WHERE (yr = 1980 AND subject = 'Physics') OR (yr = 1984 AND subject = 'Chemistry')

```

+ Show the winners for 1980 excluding the Chemistry and Medicine

```sql
	SELECT * 
	FROM nobel
	WHERE yr = 1980 AND subject NOT IN ('Chemistry', 'Medicine')
```

+ Show who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)

```sql
	SELECT * 
	FROM nobel
	WHERE (subject = 'Medicine' AND yr < 1910) OR (subject = 'Literature' AND yr > 2003)
```

+ Find all details of the prize won by PETER GRÜNBERG

```sql
	SELECT * 
	FROM nobel
	WHERE winner = 'PETER GRÜNBERG'
```

+ Find all details of the prize won by EUGENE O'NEILL

```sql
	SELECT * 
	FROM nobel
	WHERE winner = 'EUGENE O\'NEILL'
```

+ Knights in order

List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.

```sql
	SELECT winner, yr, subject
	FROM nobel
	WHERE winner LIKE 'Sir%'
	ORDER BY yr desc, winner
```

+ The expression subject IN ('Chemistry','Physics') can be used as a value - it will be 0 or 1.

Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.

```sql
	SELECT winner, subject
	FROM nobel
 	WHERE yr=1984
 	ORDER BY subject IN ('Physics','Chemistry'), subject asc, winner asc
```

### The Join Operation

+ The first example shows the goal scored by a player with the last name 'Bender'. The * says to list all the columns in the table - a shorter way of saying matchid, teamid, player, gtime

Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'

```sql
	SELECT matchid, player FROM goal 
 	WHERE teamid = 'GER'
```

+ From the previous query you can see that Lars Bender's scored a goal in game 1012. Now we want to know what teams were playing in that match. 
+ Notice in the that the column matchid in the goal table corresponds to the id column in the game table. We can look up information about game 1012 by finding that row in the game table.

Show id, stadium, team1, team2 for just game 1012

```sql
	SELECT id,stadium,team1,team2
  FROM game
	WHERE id = 1012
```

+ You can combine the two steps into a single query with a JOIN. 

+ SELECT *
  FROM game JOIN goal ON (id=matchid)
The FROM clause says to merge data from the goal table with that from the game table. The ON says how to figure out which rows in game go with which rows in goal - the id from goal must match matchid from game. (If we wanted to be more clear/specific we could say 
ON (game.id=goal.matchid)

The code below shows the player (from the goal) and stadium name (from the game table) for every goal scored.

Modify it to show the player, teamid, stadium and mdate and for every German goal.

```sql
	SELECT player, teamid, stadium, mdate
  	FROM game JOIN goal ON (id=matchid)
	WHERE teamid = 'GER'
```