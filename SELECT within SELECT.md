## SELECT within SELECT

world(name, continent, area, population, gdp)

1.
List each country name where the population is larger than that of 'Russia'.
```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia');
```
2.
Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
```sql
select name from world 
where continent = 'Europe' and gdp/population > 
(select gdp/population from world where name =  'United Kingdom');
```
3.

List the name and continent of countries in the continents containing
either Argentina or Australia. Order by name of the country.
```sql
select name,continent from world where continent IN 
(select continent from world where name IN
( 'Argentina','Australia') ) order by name;
```
4.
Which country has a population that is more than United Kingom 
but less than Germany? Show the name and the population.
```sql
SELECT name,population FROM world
WHERE population BETWEEN
(SELECT population+1 FROM world WHERE name='United Kingdom')
AND
(SELECT population-1 FROM world WHERE name='Germany');
```
5.
Show the name and the population of each country in Europe. 
Show the population as a percentage of the population of Germany.
```sql
SELECT name, CONCAT(CAST(ROUND(100*population/(SELECT population FROM world
WHERE name = 'Germany'),0) AS INT), '%')percetage
FROM world
WHERE continent = 'Europe'
```
6.
Which countries have a GDP greater than every country in Europe? 
[Give the name only.] (Some countries may have NULL gdp values)
```sql
select name from world where GDP > all(select GDP from world 
where continent = 'Europe' AND gdp > 0)
```
7.
Find the largest country (by area) in each continent, show the continent,
the name and the area:
```sql
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND area>0)
```
8.
List each continent and the name of the country that comes first alphabetically.
```sql
SELECT continent,name FROM world x
  WHERE x.name <= ALL (
    SELECT name FROM world y
     WHERE x.continent=y.continent);
```
9.
Find the continents where all countries have a population <= 25000000. 
Then find the names of the countries associated with these continents. 
Show name, continent and population.
```sql
select name,continent,population from world x 
where 25000000 >= all (select population from world y
where x.continent = y.continent and y.population >0);
```
10.
Some countries have populations more than three times that 
of all of their neighbours (in the same continent). 
Give the countries and continents.
```sql
select name, continent FROM world x where
 population > all
 (select population*3 from world y
 where y.continent = x.continent
 and y.name != x.name);
```
