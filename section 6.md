### JOIN and UEFA EURO 2012

### 1.

#### The first example shows the goal scored by a player with the last name 'Bender'. The *

#### says to list all the columns in the table - a shorter way of saying

```
matchid, teamid, player, gtime
```

#### Modify it to show the matchid and player name for all goals scored by Germany. To identify

#### German players, check for: teamid = 'GER'

```
1 SELECT matchid, player
2 FROM goal
3 WHERE teamid = 'GER'
```
### 2.

#### Show id, stadium, team1, team2 for just game 1012

```
1 SELECT id,stadium,team1,team
2 FROM game
3 WHERE id = 1012
```
### 3.

#### Modify the code to show the player, teamid, stadium and mdate for every German goal.

```
1 SELECT player, teamid, stadium, mdate
2 FROM game JOIN goal ON (id=matchid)
3 WHERE teamid = 'GER';
```
### 4.

#### Show the team1, team2 and player for every goal scored by a player called Mario

```
player LIKE 'Mario%'
1 SELECT gm.team1, gm.team2, gl.player
2 FROM goal AS gl
3 JOIN game AS gm
4 ON gl.matchid = gm.id
```

```
5 WHERE gl.player LIKE 'Mario%';
```
### 5.

#### Show player , teamid , coach , gtime for all goals scored in the first 10 minutes

```
gtime<=
1 SELECT gl.player, gl.teamid, t.coach, gl.gtime
2 FROM goal AS gl
3 JOIN eteam AS t
4 ON gl.teamid = t.id
5 WHERE gl.gtime <= 10 ;
```
### 6.

#### List the dates of the matches and the name of the team in which 'Fernando Santos' was the

#### team1 coach.

```
1 SELECT g.mdate, t.teamname
2 FROM game AS g
3 JOIN eteam AS t
4 ON g.team1 = t.id
5 WHERE t.coach = 'Fernando Santos'
```
### 7.

#### List the player for every goal scored in a game where the stadium was 'National Stadium,

#### Warsaw'

```
1 SELECT gl.player
2 FROM goal AS gl
3 JOIN game AS gm
4 ON gl.matchid = gm.id
5 WHERE gm.stadium = 'National Stadium, Warsaw';
```

### 8.

#### Show the name of all players who scored a goal against Germany.

```
1 SELECT DISTINCT gl.player
2 FROM goal AS gl
3 JOIN game AS gm
4 ON gl.matchid = gm.id
5 JOIN eteam AS t
6 ON t.id = gl.teamid
7 WHERE gl.teamid != 'GER'
8 AND 'GER' IN (gm.team1, gm.team2);
```
### 9.

#### Show teamname and the total number of goals scored.

```
1 SELECT t.teamname, COUNT(*)
2 FROM eteam AS t
3 JOIN goal AS gl
4 ON t.id=gl.teamid
5 GROUP BY t.teamname;
```
### 10.

#### Show the stadium and the number of goals scored in each stadium.

```
1 SELECT gm.stadium, COUNT(*)
2 FROM game AS gm
3 JOIN goal as gl
4 ON gl.matchid = gm.id
5 GROUP BY gm.stadium;
```

### 11.

#### For every match involving 'POL', show the matchid, date and the number of goals scored.

```
1 SELECT gm.id, gm.mdate, COUNT(*)
2 FROM game AS gm
3 JOIN goal AS gl
4 ON gm.id = gl.matchid
5 WHERE 'POL' IN (gm.team1, gm.team2)
6 GROUP BY gm.id, gm.mdate;
```
### 12.

#### For every match where 'GER' scored, show matchid, match date and the number of goals

#### scored by 'GER'

```
1 SELECT gm.id, gm.mdate, COUNT(*)
2 FROM goal AS gl
3 JOIN game AS gm
4 ON gl.matchid = gm.id
5 WHERE gl.teamid = 'GER'
6 GROUP BY gm.id, gm.mdate
7 HAVING COUNT(*) >= 1 ;
```
### 13.

#### List every match with the goals scored by each team. Sort your result by mdate, matchid,

#### team1 and team2.

##### 1 SELECT

```
2 mdate,
3 team1,
4 SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) AS score1,
5 team2,
6 SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) AS score
7 FROM game JOIN goal ON matchid = id
8 GROUP BY mdate, team1, team
```

```
9 ORDER BY mdate, matchid, team1, team2
```