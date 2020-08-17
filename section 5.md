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