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