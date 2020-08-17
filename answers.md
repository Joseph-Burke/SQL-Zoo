# Project: SQL

## Part 2: Select from 'world'

## 1. Introduction

#### Observe the result of running this SQL command to show the name, continent and

#### population of all countries.

```
SELECT name, continent, population FROM world;
```
## 2. Large Countries

#### Show the name for the countries that have a population of at least 200 million. 200 million

#### is 200000000, there are eight zeros.

```
1 SELECT name FROM world
2 WHERE population > 200 * 1000000 ;
```
## 3. Per capita GDP

#### Give the name and the per capita GDP for those countries with a population of at least

#### 200 million.

```
1 SELECT name, gdp/population AS gdp_per_capita
2 FROM world
3 WHERE population > 200000000 ;
```
## 4. South America in Millions


#### Show the name and population in millions for the countries of the continent 'South

#### America'. Divide the population by 1000000 to get population in millions.

```
1 SELECT name, population/ 1000000 AS population_in_millions
2 FROM world
3 WHERE continent = 'South America';
```
### 5. France, Germany, Italy

#### Show the name and population for France, Germany, Italy

```
1 SELECT name, population
2 FROM world
3 WHERE name IN('France', 'Germany', 'Italy');
```
### 6. United

#### Show the countries which have a name that includes the word 'United'

```
1 SELECT name
2 FROM world
3 WHERE name LIKE '%united%';
```
### 7. Two ways to be big

#### Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has

#### a population of more than 250 million.

#### Show the countries that are big by area or big by population. Show name, population and

#### area.


```
1 SELECT name, population, area
2 FROM world
3 WHERE area > 3000000
4 OR population > 250000000 ;
```
### 8. One or the other (but not both)

#### Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by

#### population (more than 250 million) but not both. Show name, population and area.

```
1 SELECT name, population, area
2 FROM world
3 WHERE area > 3000000
4 XOR population > 250000000 ;
```
### 9. Rounding

#### Show the name and population in millions and the GDP in billions for the countries of

#### the continent 'South America'. Use the ROUND function to show the values to two

#### decimal places.

##### 1 SELECT

```
2 name,
3 ROUND(population / 1000000 , 2 ),
4 ROUND(gdp / 1000000000 , 2 )
5 FROM world
6 WHERE continent = 'South America';
```
### 10. Trillion dollar economies

#### Show the name and per-capita GDP for those countries with a GDP of at least one trillion

#### (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

#### Show per-capita GDP for the trillion dollar countries to the nearest $1000.


##### 1 SELECT

```
2 name,
3 ROUND(gdp / population, - 3 )
4 FROM world
5 WHERE gdp > 1000000000000 ;
```
### 11. Name and capital have the same length

#### Show the name and capital where the name and the capital have the same number of

#### characters.

```
1 SELECT name, capital
2 FROM world
3 WHERE LENGTH(name) = LENGTH(capital);
```
### 12. Matching name and capital

#### Show the name and the capital where the first letters of each match. Don't include countries

#### where the name and the capital are the same word.

```
1 SELECT name, capital
2 FROM world
3 WHERE LEFT(name, 1 ) = LEFT(capital, 1 )
4 AND name != capital;
```
### 13. All the vowels

#### Equatorial Guinea and Dominican Republic have all of the vowels (a e i o u) in the name.

#### They don't count because they have more than one word in the name.

#### Find the country that has all the vowels and no spaces in its name.


```
1 SELECT name
2 FROM world
3 WHERE
4 name NOT LIKE '% %'
5 AND name LIKE '%a%'
6 AND name LIKE '%e%'
7 AND name LIKE '%i%'
8 AND name LIKE '%o%'
9 AND name LIKE '%u%';
```
## Part 3: Select from 'nobel'

### 1. Winners from 1950

#### Change the query shown so that it displays Nobel prizes for 1950.

```
1 SELECT yr, subject, winner
2 FROM nobel
3 WHERE yr = 1950 ;
```
### 2. 1962 Literature

#### Show who won the 1962 prize for Literature.

```
1 SELECT winner
2 FROM nobel
3 WHERE yr = 1962
4 AND subject = 'Literature';
```
### 3. Albert Einstein

#### Show the year and subject that won 'Albert Einstein' his prize.


```
1 SELECT yr, subject
2 FROM nobel
3 WHERE winner = 'Albert Einstein';
```
### 4. Recent Peace Prizes

#### Give the name of the 'Peace' winners since the year 2000, including 2000.

```
1 SELECT winner
2 FROM nobel
3 WHERE
4 yr >= 2000
5 AND subject = 'Peace';
```
### 5. Literature in the 1980's

#### Show all details ( yr , subject , winner ) of the Literature prize winners for 1980 to 1989

#### inclusive.

```
1 SELECT yr, subject, winner
2 FROM nobel
3 WHERE subject = 'Literature'
4 AND yr BETWEEN 1980 AND 1989 ;
```
### 6. Only Presidents

#### Show all details of the presidential winners:

#### Theodore Roosevelt

#### Woodrow Wilson

#### Jimmy Carter

#### Barack Obama


```
1 SELECT * FROM nobel
2 WHERE winner IN (
3 'Theodore Roosevelt',
4 'Woodrow Wilson',
5 'Jimmy Carter',
6 'Barack Obama'
7 );
```
### 7. John

#### Show the winners with first name John

```
1 SELECT winner
2 FROM nobel
3 WHERE winner LIKE 'John %';
```
### 8. Chemistry and Physics from different years

#### Show the year, subject, and name of Physics winners for 1980 together with the Chemistry

#### winners for 1984.

```
1 SELECT yr, subject, winner
2 FROM nobel
3 WHERE subject = 'Physics' AND yr = 1980
4 OR subject = 'Chemistry' AND yr = 1984 ;
```
### 9. Exclude Chemists and Medics

#### Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine

```
1 SELECT yr, subject, winner
2 FROM nobel
3 WHERE yr = 1980
4 AND subject NOT IN ('Chemistry', 'Medicine');
```

### 10. Early Medicine, Late Literature

#### Show year, subject, and name of people who won a 'Medicine' prize in an early year (before

#### 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after

#### 2004, including 2004)

```
1 SELECT yr, subject, winner
2 FROM nobel
3 WHERE subject = 'Medicine' AND yr < 1910
4 OR subject = 'Literature' AND yr >= 2004 ;
```
### 11. Umlaut

#### Find all details of the prize won by PETER GRÜNBERG

##### 1 SELECT *

```
2 FROM nobel
3 WHERE winner = 'Peter Grünberg';
```
### 12. Apostrophe

#### Find all details of the prize won by EUGENE O'NEILL

##### 1 SELECT *

```
2 FROM nobel
3 WHERE winner = 'Eugene O\'Neill'
```
### 13. Knights of the realm

#### List the winners, year and subject where the winner starts with Sir. Show the the most

#### recent first, then by name order.


```
1 SELECT winner, yr, subject
2 FROM nobel
3 WHERE winner LIKE 'Sir%';
```
### 14. Chemistry and Physics last

#### Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry

#### and Physics last.

```
1 SELECT winner, subject
2 FROM nobel
3 WHERE yr = 1984
4 ORDER BY subject IN ('Chemistry', 'Physics'), subject, winner
```
## SELECT in SELECT quiz

### 1. Bigger than Russia

#### List each country name where the population is larger than that of 'Russia'.

```
1 SELECT name
2 FROM world
3 WHERE population > (
4 SELECT population FROM world WHERE name = 'Russia'
5 );
```
### 2. Richer than UK

#### Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.


```
1 SELECT name
2 FROM world
3 WHERE continent = 'Europe'
4 AND gdp/population > (
5 SELECT gdp/population
6 FROM world
7 WHERE name = 'United Kingdom'
8 );
```
### 3. Neighbours of Argentina and Australia

#### List the name and continent of countries in the continents containing either Argentina or

#### Australia. Order by name of the country.

```
1 SELECT name, continent
2 FROM world
3 WHERE continent IN (
4 SELECT continent
5 FROM world
6 WHERE name IN ('Argentina', 'Australia')
7 )
8 ORDER BY name;
```
### 4. Between Canada and Poland

#### Which country has a population that is more than Canada but less than Poland? Show the

#### name and the population.

##### 1 SELECT *

```
2 FROM world
3 WHERE
4 population > (
5 SELECT population
6 FROM world
7 WHERE name = 'Canada'
8 )
9 AND
10 population < (
11 SELECT population
```

```
12 FROM world
13 WHERE name = 'Poland'
14 );
```
### 5. Percentages of Germany

#### Germany (population 80 million) has the largest population of the countries in Europe.

#### Austria (population 8.5 million) has 11% of the population of Germany.

#### Show the name and the population of each country in Europe. Show the population as a

#### percentage of the population of Germany.

##### 1 SELECT

```
2 name,
3 CONCAT(
4 ROUND(
5 population / (
6 SELECT population
7 FROM world
8 WHERE name = 'Germany'
9 ) * 100 , 0 ),
10 '%'
11 ) AS percentage
12 FROM world
13 WHERE continent = 'Europe';
```
### 6. Bigger than every country in Europe

#### Which countries have a GDP greater than every country in Europe? [Give the name only.]

#### (Some countries may have NULL gdp values)

```
1 SELECT name
2 FROM world
3 WHERE gdp > ALL(
4 SELECT gdp
5 FROM world
6 WHERE continent = 'Europe'
7 AND gdp > 0
8 );
```

### 7. Largest in each continent

#### Find the largest country (by area) in each continent, show the continent , the name and the

#### area :

```
1 SELECT continent, name, area
2 FROM world AS w
3 WHERE area >= ALL(SELECT area
4 FROM world AS w
5 WHERE w1.continent = w2.continent
6 AND area > 0
7 );
```
### 8. First country of each continent (alphabetically)

#### List each continent and the name of the country that comes first alphabetically.

```
1 SELECT continent, name
2 FROM world AS w
3 WHERE name <= ALL(SELECT name
4 FROM world AS w
5 WHERE w1.continent = w2.continent
6 AND w2.name >= 'a');
```
### 9. Difficult Questions That Utilize Techniques Not Covered In Prior

### Sections

#### Find the continents where all countries have a population <= 25000000. Then find the

#### names of the countries associated with these continents. Show name , continent and

#### population.

```
1 SELECT name, continent, population
2 FROM world AS w
```

```
3 WHERE 25000000 >= ALL(SELECT population
4 FROM world AS w
5 WHERE w1.continent = w2.continent
6 AND w2.population > 0 );
```
### 10. Difficult Questions That Utilize Techniques Not Covered In Prior

### Sections

#### Some countries have populations more than three times that of any of their neighbours (in

#### the same continent). Give the countries and continents.

```
1 SELECT name, continent
2 FROM world AS w
3 WHERE population/ 3 >= ALL(
4 SELECT population
5 FROM world AS w
6 WHERE w1.continent = w2.continent
7 AND w1.name != w2.name
8 );
```
## SUM and COUNT

### 1. Total world population

#### Show the total population of the world.

```
1 SELECT SUM(population)
2 FROM world
```
### 2. List of continents

#### List all the continents - just once each.


```
1 SELECT DISTINCT continent
2 FROM world;
```
### 3. GDP of Africa

#### Give the total GDP of Africa

```
1 SELECT SUM(gdp)
2 FROM world
3 WHERE continent = 'Africa';
```
### 4. Count the big countries

#### How many countries have an area of at least 1000000

##### 1 SELECT COUNT(*)

```
2 FROM world
3 WHERE area >= 1000000 ;
```
### 5. Baltic states population

#### What is the total population of ('Estonia', 'Latvia', 'Lithuania')

```
1 SELECT SUM(population)
2 FROM world
3 WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```
### 6. Counting the countries of each continent

#### For each continent show the continent and number of countries.


```
1 SELECT continent, COUNT(*)
2 FROM world
3 GROUP BY continent;
```
### 7. Counting big countries in each continent

#### For each continent show the continent and number of countries with populations of at

#### least 10 million.

```
1 SELECT continent, COUNT(*)
2 FROM world
3 WHERE population >= 10 * 1000000
4 GROUP BY continent;
```
### 8. Counting big continents

#### List the continents that have a total population of at least 100 million.

```
1 SELECT continent
2 FROM world
3 GROUP BY continent
4 HAVING SUM(population) >= 100000000 ;
```
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
### More JOIN Operations

### 1. 1962 movies

#### List the films where the yr is 1962 [Show id , title ]

```
SELECT id, title FROM movie WHERE yr= 1962 ;
```
### 2. When was Citizen Kane released?

#### Give year of 'Citizen Kane'.

```
SELECT yr FROM movie WHERE title = 'Citizen Kane';
```
### 3. Star Trek movies

#### List all of the Star Trek movies, include the id , title and yr (all of these movies include the

#### words Star Trek in the title). Order results by year.

```
SELECT id, title, yr FROM movie WHERE title LIKE '%Star Trek%' ORDER BY yr;
```
### 4. id for actor Glenn Close

#### What id number does the actor 'Glenn Close' have?

##### INSERT CODE


### 5. id for Casablanca

#### What is the id of the film 'Casablanca'?

```
SELECT id FROM movie WHERE title = 'Casablanca';
```
### 6. Cast list for Casablanca

#### Obtain the cast list for 'Casablanca'.

#### Use movieid=11768 , (or whatever value you got from the previous question)

```
1 SELECT name
2 FROM actor AS a
3 JOIN casting AS c ON c.actorid = a.id
4 WHERE movieid = 11768 ;
```
### 7. Alien cast list

#### Obtain the cast list for the film 'Alien'

```
1 SELECT actor.name
2 FROM actor
3 JOIN casting
4 ON actor.id = casting.actorid
5 JOIN movie
6 ON movie.id = casting.movieid
7 WHERE movie.title = 'Alien';
```
### 8. Harrison Ford movies

#### List the films in which 'Harrison Ford' has appeared


```
1 SELECT title
2 FROM movie
3 JOIN casting
4 ON casting.movieid = movie.id
5 JOIN actor
6 ON actor.id = casting.actorid
7 WHERE actor.name = 'Harrison Ford';
```
### 9. Harrison Ford as a supporting actor

#### List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the ord

#### field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]

```
1 SELECT title
2 FROM movie
3 JOIN casting
4 ON casting.movieid = movie.id
5 JOIN actor
6 ON actor.id = casting.actorid
7 WHERE actor.name = 'Harrison Ford'
8 AND casting.ord != 1 ;
```
### 10. Lead actors in 1962 movies

#### List the films together with the leading star for all 1962 films.

```
1 SELECT movie.title, actor.name
2 FROM movie
3 JOIN casting ON movie.id = casting.movieid
4 JOIN actor ON actor.id = casting.actorid
5 WHERE movie.yr = 1962 AND casting.ord = 1 ;
```
### 11. Busy years for Rock Hudson

#### INSERT INSTRUCTIONS


```
1 SELECT yr,COUNT(title) FROM
2 movie JOIN casting ON movie.id=movieid
3 JOIN actor ON actorid=actor.id
4 WHERE name='Rock Hudson'
5 GROUP BY yr
6 HAVING COUNT(title) > 2 ;
```
### 12. Lead actor in Julie Andrews movie

#### List the film title and the leading actor for all of the films 'Julie Andrews' played in.

```
1 SELECT movie.title, actor.name FROM movie
2 JOIN casting ON movie.id = casting.movieid
3 JOIN actor ON actor.id = casting.actorid
4 WHERE movie.id IN (
5 SELECT casting.movieid
6 FROM casting
7 JOIN actor ON casting.actorid = actor.id
8 WHERE actor.name = 'Julie Andrews'
9 ) AND casting.ord = 1 ;
```
### 13. Actors with 15 leading roles

#### Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.

```
1 SELECT actor.name
2 FROM casting
3 JOIN actor ON actor.id = casting.actorid
4 WHERE ord = 1
5 GROUP BY actor.name HAVING COUNT(*) >= 15 ;
```
### 14.

#### List the films released in the year 1978 ordered by the number of actors in the cast, then by

#### title.


```
1 SELECT movie.title, COUNT(*)
2 FROM casting
3 JOIN movie ON movie.id = casting.movieid
4 WHERE movie.yr = 1978
5 GROUP BY casting.movieid, movie.title
6 ORDER BY COUNT(*) DESC, title;
```
### 15.

#### List the films released in the year 1978 ordered by the number of actors in the cast, then by

#### title.

```
1 SELECT actor.name FROM actor
2 JOIN casting ON actor.id = casting.actorid
3 WHERE casting.movieid IN (
4 SELECT casting.movieid
5 FROM casting WHERE casting.actorid = (
6 SELECT actor.id
7 FROM actor
8 WHERE actor.name = 'Art Garfunkel'))
9 AND actor.name != 'Art Garfunkel';
```
### NULL, INNER JOIN, LEFT JOIN, RIGHT JOIN

### 1.

#### List the teachers who have NULL for their department.

```
SELECT name FROM teacher WHERE dept IS NULL
```
### 2.

#### Note the INNER JOIN misses the teachers with no department and the departments with no

#### teacher.


```
1 SELECT teacher.name, dept.name
2 FROM teacher INNER JOIN dept
3 ON (teacher.dept=dept.id)
```
### 3.

#### Use a different JOIN so that all teachers are listed.

```
1 SELECT t.name, d.name FROM teacher AS t
2 LEFT JOIN dept AS d
3 ON t.dept = d.id;
```
### 4.

#### Use a different JOIN so that all departments are listed.

```
1 SELECT t.name, d.name FROM teacher AS t
2 RIGHT JOIN dept AS d
3 ON d.id = t.dept;
```
### 5.

#### Use COALESCE to print the mobile number. Use the number '07986 444 2266' if there is no

#### number given. Show teacher name and mobile number or '07986 444 2266'

```
1 SELECT t.name, COALESCE(mobile, '07986 444 2266')
2 FROM teacher AS t;
```
### 6.


#### Use the COALESCE function and a LEFT JOIN to print the teacher name and department

#### name. Use the string 'None' where there is no department.

```
1 SELECT t.name, COALESCE(d.name, 'None')
2 FROM teacher AS t
3 LEFT JOIN dept AS d ON t.dept = d.id;
```
### 7.

#### Use COUNT to show the number of teachers and the number of mobile phones.

```
SELECT COUNT(id), COUNT(mobile) FROM teacher;
```
### 8.

#### Use COUNT and GROUP BY dept.name to show each department and the number of staff.

#### Use a RIGHT JOIN to ensure that the Engineering department is listed.

```
1 SELECT dept.name, COUNT(teacher.id)
2 FROM teacher
3 RIGHT JOIN dept
4 ON dept.id = teacher.dept
5 GROUP BY dept.name;
```
### 9.

#### Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2

#### and 'Art' otherwise.

```
1 SELECT name, CASE WHEN dept = 1
2 THEN 'Sci'
3 WHEN dept = 2 THEN 'Sci'
```

```
4 ELSE 'Art'
5 END
6 FROM teacher;
```
### 10.

#### Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2,

#### show 'Art' if the teacher's dept is 3 and 'None' otherwise.

```
1 SELECT name, CASE WHEN dept = 1 OR dept = 2 THEN 'Sci'
2 WHEN dept = 3 THEN 'Art'
3 ELSE 'None'
4 END
5 FROM teacher;
```
### SELF JOIN

### 1.

#### How many stops are in the database.

```
SELECT name FROM teacher WHERE dept IS NULL
```
### 2.

#### Find the id value for the stop 'Craiglockhart'

```
SELECT id FROM stops WHERE name = 'Craiglockhart';
```
### 3.


#### Give the id and the name for the stops on the '4' 'LRT' service.

```
1 SELECT s.id, s.name FROM route AS r
2 JOIN stops AS s ON r.stop = s.id
3 WHERE r.num = 4 AND r.company = 'LRT'
4 ORDER BY r.pos;
```
### 4. Routes and stops

#### The query shown gives the number of routes that visit either London Road (149) or

#### Craiglockhart (53). Run the query and notice the two services that link these stops have a

#### count of 2. Add a HAVING clause to restrict the output to these two routes.

```
1 SELECT company, num, COUNT(*)
2 FROM route WHERE stop= 149 OR stop= 53
3 GROUP BY company, num HAVING COUNT(*) > 1 ;
```
### 5.

#### Execute the self join shown and observe that b.stop gives all the places you can get to from

#### Craiglockhart, without changing routes. Change the query so that it shows the services from

#### Craiglockhart to London Road.

```
1 SELECT a.company, a.num, a.stop, b.stop
2 FROM route a JOIN route b ON
3 (a.company=b.company AND a.num=b.num)
4 WHERE a.stop= 53 AND b.stop = (SELECT stops.id FROM stops WHERE stops.name
```
### 6.

#### The query shown is similar to the previous one, however by joining two copies of the stops

#### table we can refer to stops by name rather than by number. Change the query so that the


#### services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these

#### places try 'Fairmilehead' against 'Tollcross'

```
1 SELECT a.company, a.num, stopa.name, stopb.name
2 FROM route a JOIN route b ON
3 (a.company=b.company AND a.num=b.num)
4 JOIN stops stopa ON (a.stop=stopa.id)
5 JOIN stops stopb ON (b.stop=stopb.id)
6 WHERE stopa.name='Craiglockhart'
7 AND stopb.name='London Road'
```
### 7.

#### Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith')

```
1 SELECT DISTINCT r1.company, r1.num FROM route AS r1
2 JOIN route AS r2 ON (r1.num, r1.company) = (r2.num, r2.company)
3 WHERE r1.stop = 115 AND r2.stop = 137 ;
```
### 8.

#### Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'

```
1 SELECT DISTINCT r1.company, r1.num FROM route AS r1
2 JOIN route AS r2 ON (r1.num, r1.company) = (r2.num, r2.company)
3 WHERE r1.stop = (SELECT id FROM stops WHERE stops.name = 'Craiglockhart')
4 AND r2.stop = (SELECT id FROM stops WHERE stops.name = 'Tollcross');
```
### 9.

#### Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one

#### bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and

#### bus no. of the relevant services.


```
1 SELECT s.name, r1.company, r1.num
2 FROM route AS r1
3 JOIN route AS r2
4 ON (r1.num, r1.company) = (r2.num, r2.company)
5 JOIN stops AS s ON s.id = r2.stop
6 WHERE r1.stop = (SELECT id FROM stops WHERE name = 'Craiglockhart')
7 AND r1.company = 'LRT';
```
### 10.

#### Find the routes involving two buses that can go from Craiglockhart to Lochend.

#### Show the bus no. and company for the first bus, the name of the stop for the transfer,

#### and the bus no. and company for the second bus.

```
1 SELECT r1.num, r1.company, s.name, r3.num, r3.company FROM route r1
2 JOIN route AS r2 ON (r1.num, r1.company) = (r2.num, r2.company)
3 JOIN route AS r3 ON (r2.stop) = (r3.stop)
4 JOIN route AS r4 ON (r3.num, r3.company) = (r4.num, r4.company)
5 JOIN stops AS s ON (s.id = r2.stop)
6 WHERE r1.stop = (SELECT stops.id FROM stops WHERE name = 'Craiglockhart')
7 AND r4.stop = (SELECT stops.id FROM stops WHERE name = 'Lochend')
8 ORDER BY r1.num, s.name, r3.num;
```

