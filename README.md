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