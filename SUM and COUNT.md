## SUM and COUNT

world(name, continent, area, population, gdp)
1.
Show the total population of the world.
```sql
SELECT SUM(population)
FROM world;
```
2.
List all the continents - just once each.
```sql
SELECT distinct(continent)
FROM world;
```
3.
Give the total GDP of Africa
```sql
SELECT SUM(gdp)
FROM world where continent = 'Africa';
```
4.
How many countries have an area of at least 1000000
```sql
select count(distinct(name)) from world where area >= 1000000; 
```
5.
What is the total population of ('Estonia', 'Latvia', 'Lithuania')
```sql
select sum(population) from world where name IN ('Estonia', 'Latvia', 'Lithuania');
```
6.
For each continent show the continent and number of countries.
```sql
7.
For each continent show the continent and number of countries with populations of at least 10 million.
```
8.
List the continents that have a total population of at least 100 million.
```sql
select continent from world group by continent having sum(population) > 100000000 ;
```

