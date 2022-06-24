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

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```
