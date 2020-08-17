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