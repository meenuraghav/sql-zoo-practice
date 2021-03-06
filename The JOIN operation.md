## The JOIN operation

1.
show the matchid and player name for all goals scored by Germany.
To identify German players, check for: teamid = 'GER'
```sql
SELECT matchid,player FROM goal WHERE teamid = 'GER' ;
```
2.
Show id, stadium, team1, team2 for just game 1012
```sql
SELECT id,stadium,team1,team2
  FROM game
  WHERE id = 1012;
```
3.
Modify it to show the player, teamid, stadium and mdate for every German goal.
```sql
SELECT player, teamid, stadium, mdate
  FROM game JOIN goal ON (id=matchid) where goal.teamid = 'GER' ;
```
4.
Use the same JOIN as in the previous question.

Show the team1, team2 and player for every goal scored by 
a player called Mario player LIKE 'Mario%'
```sql
SELECT g.team1,g.team2,gl.player FROM game as g JOIN goal as gl 
ON g.id = gl.matchid where gl.player LIKE 'Mario%' ;
```
5.
Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10
```sql
SELECT player, teamid, coach,gtime
  FROM goal JOIN eteam on teamid=id
 WHERE gtime<=10 ;
```
6.
List the dates of the matches and the name of the team
in which 'Fernando Santos' was the team1 coach.
```sql
SELECT mdate,teamname FROM game JOIN eteam ON (team1=eteam.id) WHERE coach = 'Fernando Santos';
```
7.
List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'
```sql
SELECT player FROM goal JOIN game ON (matchid=id) WHERE stadium = 'National Stadium, Warsaw' ;
```
8.
Instead show the name of all players who scored a goal against Germany.
```sql
SELECT DISTINCT(player)
  FROM game JOIN goal ON id = id 
    WHERE (team1='GER' OR team2='GER')
    AND teamid <>'GER' ;
```
9.
Show teamname and the total number of goals scored.
```sql
SELECT teamname, COUNT(matchid)
  FROM eteam JOIN goal ON id=teamid
 GROUP BY teamname
 ORDER BY teamname ;
```
10.
Show the stadium and the number of goals scored in each stadium.
```sql
SELECT stadium,COUNT(matchid) 
 FROM game JOIN goal ON id = matchid 
 GROUP BY stadium ;
```
11.
For every match involving 'POL', show the matchid, date and the number of goals scored.
```sql
SELECT matchid,mdate, COUNT(matchid)
  FROM game JOIN goal ON matchid = id 
 WHERE (team1 = 'POL' OR team2 = 'POL')
 GROUP BY matchid, mdate ;
```
12.
For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'
```sql
SELECT matchid, mdate, COUNT(matchid)
 FROM game JOIN goal ON matchid = id
  WHERE (team1='GER' OR team2='GER')
  AND teamid = 'GER' 
  GROUP BY matchid,mdate ;
```
13.
List every match with the goals scored by each team as shown.
This will use "CASE WHEN" which has not been explained in any previous exercises.
Notice in the query given every goal is listed. If it was a team1 goal then a 1 appears in score1, otherwise there is a 0. 
You could SUM this column to get a count of the goals scored by team1. Sort your result by mdate, matchid, team1 and team2.
```sql
SELECT mdate, team1, 
SUM(CASE WHEN teamid = team1 THEN 1 ELSE 0 END) score1,
team2,
SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) score2
FROM game LEFT JOIN goal ON matchid = id
GROUP BY mdate, team1, team2
```

