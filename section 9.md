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