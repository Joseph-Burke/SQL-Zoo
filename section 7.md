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