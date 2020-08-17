## The JOIN operation

### 1.

#### The first example shows the goal scored by a player with the last name 'Bender'. The * says to list all the columns in the table - a shorter way of saying

```
matchid, teamid, player, gtime
```

#### Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'

```
SELECT matchid, player
FROM goal
WHERE teamid = 'GER'
```
### 2.

#### Show id, stadium, team1, team2 for just game 1012

```
SELECT id, stadium, team1, team2
FROM game
WHERE id = 1012;
```
### 3.

#### Modify the code to show the player, teamid, stadium and mdate for every German goal.

```
SELECT player, teamid, stadium, mdate
FROM game JOIN goal ON (id=matchid)
WHERE teamid = 'GER';
```
### 4.

#### Show the team1, team2 and player for every goal scored by a player called Mario

```
SELECT gm.team1, gm.team2, gl.player
FROM goal AS gl
JOIN game AS gm
ON gl.matchid = gm.id;
WHERE gl.player LIKE 'Mario%';
```
### 5.

#### Show player, teamid, coach, gtime for all goals scored in the first 10 minutes.

```
SELECT gl.player, gl.teamid, t.coach, gl.gtime
FROM goal AS gl
JOIN eteam AS t
ON gl.teamid = t.id
WHERE gl.gtime <= 10;
```
### 6.

#### List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

```
SELECT g.mdate, t.teamname
FROM game AS g
JOIN eteam AS t
ON g.team1 = t.id
WHERE t.coach = 'Fernando Santos';
```
### 7.

#### List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'.

```
SELECT gl.player
FROM goal AS gl
JOIN game AS gm
ON gl.matchid = gm.id
WHERE gm.stadium = 'National Stadium, Warsaw';
```

### 8.

#### Show the name of all players who scored a goal against Germany.

```
SELECT DISTINCT gl.player
FROM goal AS gl
JOIN game AS gm
ON gl.matchid = gm.id
JOIN eteam AS t
ON t.id = gl.teamid
WHERE gl.teamid != 'GER'
AND 'GER' IN (gm.team1, gm.team2);
```
### 9.

#### Show teamname and the total number of goals scored.

```
SELECT t.teamname, COUNT(*)
FROM eteam AS t
JOIN goal AS gl
ON t.id=gl.teamid
GROUP BY t.teamname;
```
### 10.

#### Show the stadium and the number of goals scored in each stadium.

```
SELECT gm.stadium, COUNT(*)
FROM game AS gm
JOIN goal as gl
ON gl.matchid = gm.id
GROUP BY gm.stadium;
```

### 11.

#### For every match involving 'POL', show the matchid, date and the number of goals scored.

```
SELECT gm.id, gm.mdate, COUNT(*)
FROM game AS gm
JOIN goal AS gl
ON gm.id = gl.matchid
WHERE 'POL' IN (gm.team1, gm.team2)
GROUP BY gm.id, gm.mdate;
```
### 12.

#### For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'

```
SELECT gm.id, gm.mdate, COUNT(*)
FROM goal AS gl
JOIN game AS gm
ON gl.matchid = gm.id
WHERE gl.teamid = 'GER'
GROUP BY gm.id, gm.mdate
HAVING COUNT(*) >= 1;
```
### 13.

#### List every match with the goals scored by each team. Sort your result by mdate, matchid, team1 and team2.

```
SELECT
  mdate,
  team1,
  SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) AS score1, team2,
  SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) AS score
FROM game JOIN goal ON matchid = id
GROUP BY mdate, team1, team
9 ORDER BY mdate, matchid, team1, team2;
```