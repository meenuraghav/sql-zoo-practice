## SELECT from WORLD

1. 
Show the name, continent and population of all countries.

```sql
SELECT name, continent, population FROM world;
```
2.
How to use WHERE to filter records. Show the name for the countries that have a population of at least 200 million.
200 million is 200000000, there are eight zeros.

```sql
SELECT name FROM world
WHERE population >200000000;
```
3.
Give the name and the per capita GDP for those countries with a population of at least 200 million.
```sql
select name,GDP/population from world where population>200000000
```
4.
Show the name and population in millions for the countries of the continent 'South America'.
Divide the population by 1000000 to get population in millions.
```sql
Select name,population/1000000 from world where continent='South America';
```
5.
Show the name and population for France, Germany, Italy
```sql
select name,population from world where name in ('France','Germany','Italy');
```
6.
Show the countries which have a name that includes the word 'United'
```sql
select name from world where name like '%United%';
```
7.
Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.

Show the countries that are big by area or big by population. Show name, population and area.
```sql
select name,population,area from world where area>=3000000 or population>=250000000;
```
8.
Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or 
big by population (more than 250 million) but not both. Show name, population and area.

Australia has a big area but a small population, it should be included.
Indonesia has a big population but a small area, it should be included.
China has a big population and big area, it should be excluded.
United Kingdom has a small population and a small area, it should be excluded.
```sql
select name,population,area from world WHERE ((population > 250000000) XOR (area > 3000000));
```
9.
Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. 
Use the ROUND function to show the values to two decimal places.

For South America show population in millions and GDP in billions both to 2 decimal places.
```sql
select name,round(population/1000000,2),round(GDP/1000000000,2) from world where continent='South America';
```
10.
Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros).
Round this value to the nearest 1000.
```sql
select name,round(GDP/population,-3) from world where GDP>1000000000000;
```
11.
Greece has capital Athens.

Each of the strings 'Greece', and 'Athens' has 6 characters.

Show the name and capital where the name and the capital have the same number of characters.
```sql
SELECT name,capital
  FROM world
 WHERE LENGTH(name)=LENGTH(capital);
```
12.
The capital of Sweden is Stockholm. Both words start with the letter 'S'.

Show the name and the capital where the first letters of each match. 
Don't include countries where the name and the capital are the same word.

```sql
SELECT name,capital
FROM world WHERE LEFT(name,1)=LEFT(capital,1) ans name=capital;
```
13.
Equatorial Guinea and Dominican Republic have all of the vowels (a e i o u) in the name. 
They don't count because they have more than one word in the name.

Find the country that has all the vowels and no spaces in its name.
```sql
SELECT name
   FROM world
WHERE name LIKE '%a%' and 
name LIKE '%e%' and
name LIKE '%i%' and
name LIKE '%o%' and 
name LIKE '%u%'
  AND name NOT LIKE '% %'
```
