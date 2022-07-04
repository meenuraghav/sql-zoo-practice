## More JOIN operations

1.
List the films where the yr is 1962 [Show id, title]
```sql
SELECT id, title
 FROM movie
 WHERE yr=1962
```
When was Citizen Kane released?
2.
Give year of 'Citizen Kane'.
```sql
SELECT yr FROM movie WHERE title =  'Citizen Kane' ;
```
3.
List all of the Star Trek movies, include the id, title and yr (all of these movies include the 
words Star Trek in the title). Order results by year.
```sql
SELECT id,title,yr FROM movie WHERE title LIKE 'Star Trek%' ORDER BY yr ;
```
4.
What id number does the actor 'Glenn Close' have?
```sql
SELECT id FROM actor WHERE name =  'Glenn Close' ;
```
5.
What is the id of the film 'Casablanca'
```sql
SELECT id FROM movie WHERE title =  'Casablanca' ;
```
6.
Obtain the cast list for 'Casablanca'.
```sql
SELECT actor.name FROM actor JOIN casting ON actor.id=casting.actorid 
JOIN movie ON casting.movieid =movie.id WHERE movie.title =  'Casablanca';
```
7.
Obtain the cast list for the film 'Alien'
```sql
SELECT actor.name FROM actor JOIN casting ON actor.id=casting.actorid 
JOIN movie ON casting.movieid =movie.id WHERE movie.title = 'Alien' ;
```
8.
List the films in which 'Harrison Ford' has appeared
```sql
SELECT movie.title FROM actor JOIN casting ON actor.id=casting.actorid 
JOIN movie ON casting.movieid =movie.id WHERE actor.name = 'Harrison Ford' ;
```
9.
List the films where 'Harrison Ford' has appeared - but not in the starring role. 
[Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]
```sql
SELECT movie.title FROM actor JOIN casting ON actor.id=casting.actorid 
JOIN movie ON casting.movieid =movie.id WHERE actor.name = 'Harrison Ford' AND casting.ord != 1 ;
```
10.
List the films together with the leading star for all 1962 films
```sql
SELECT movie.title,actor.name FROM actor JOIN casting ON actor.id=casting.actorid 
JOIN movie ON casting.movieid =movie.id WHERE movie.yr = 1962 AND casting.ord = 1;
```
11.
Which were the busiest years for 'Rock Hudson', show the year and the number of movies he 
made each year for any year in which he made more than 2 movies.
```sql
SELECT yr,COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
        JOIN actor   ON actorid=actor.id
WHERE name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) >1
ORDER BY COUNT(title) DESC

```
12.
List the film title and the leading actor for all of the films 'Julie Andrews' played in.
```sql
SELECT title, name 
FROM 
   movie  JOIN casting ON movie.id=movieid
          JOIN actor   ON actorid=actor.id
WHERE ord = 1 AND movieid IN ( SELECT movieid 
                               FROM casting JOIN actor
                               ON actorid = actor.id
                               WHERE name = 'Julie Andrews') 
```
13.
Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles
```sql
SELECT name FROM actor JOIN casting ON id = actorid AND ord = 1 GROUP BY name 
HAVING COUNT(name) >= 15;
```
14.
List the films released in the year 1978 ordered by the number of actors in the cast, then by title.
```sql
SELECT movie.title, COUNT(*) FROM movie JOIN casting ON movie.id = casting.movieid 
WHERE movie.yr = 1978 GROUP BY movie.title ORDER BY COUNT(actorid) DESC, title
```
15.
List all the people who have worked with 'Art Garfunkel'.
```sql
SELECT distinct actor.name
FROM movie
JOIN casting
ON casting.movieid = movie.id
JOIN actor
ON actor.id = casting.actorid
where movie.id in (select movieid from casting join actor on id =actorid where 
actor.name = 'Art Garfunkel') and actor.name <> 'Art Garfunkel'
```
