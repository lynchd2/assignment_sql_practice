### Select Basics 

1. Modify it to show the population of Germany
```sql

  SELECT population 
  FROM world
  WHERE name = 'Germany'

```

2. Show the name and the population for 'Ireland', 'Iceland' and 'Denmark'.


```sql

  SELECT name, population 
  FROM world
  WHERE name IN ('Ireland', 'Iceland', 'Denmark');

```

3. Just the right size


```sql

  SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000

```

### Select from World

1.

```sql

  SELECT name, continent, population 
  FROM world

```

2.

```sql

  SELECT name, continent, population 
  FROM world

```

3.

```sql


SELECT name, gdp / population as per_capita
FROM world
WHERE population > 200000000


```

4.

```sql

SELECT name, population as pop_in_millions
FROM world
WHERE continent = 'South America'

```
