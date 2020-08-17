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