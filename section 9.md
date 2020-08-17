### SELF JOIN

### 1.

#### How many stops are in the database.

```
SELECT COUNT(*) FROM stops;
```
### 2.

#### Find the id value for the stop 'Craiglockhart'

```
SELECT id FROM stops WHERE name = 'Craiglockhart';
```
### 3.

#### Give the id and the name for the stops on the '4' 'LRT' service.

```
SELECT s.id, s.name FROM route AS r
JOIN stops AS s ON r.stop = s.id
WHERE r.num = 4 AND r.company = 'LRT'
ORDER BY r.pos;
```
### 4. Routes and stops

#### The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.

```
SELECT company, num, COUNT(*)
FROM route WHERE stop= 149 OR stop= 53
GROUP BY company, num HAVING COUNT(*) > 1;
```
### 5.

#### Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.

```
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
(a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop = (SELECT stops.id FROM stops WHERE stops.name = 'London Road');
```
### 6.

#### The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'

```
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
(a.company=b.company AND a.num=b.num)
JOIN stops stopa ON (a.stop=stopa.id)
JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart'
AND stopb.name='London Road'
```
### 7.

#### Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith')

```
SELECT DISTINCT r1.company, r1.num FROM route AS r1
JOIN route AS r2 ON (r1.num, r1.company) = (r2.num, r2.company)
WHERE r1.stop = 115 AND r2.stop = 137;
```
### 8.

#### Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'

```
SELECT DISTINCT r1.company, r1.num FROM route AS r1
JOIN route AS r2 ON (r1.num, r1.company) = (r2.num, r2.company)
WHERE r1.stop = (SELECT id FROM stops WHERE stops.name = 'Craiglockhart')
AND r2.stop = (SELECT id FROM stops WHERE stops.name = 'Tollcross');
```
### 9.

#### Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.

```
SELECT s.name, r1.company, r1.num
FROM route AS r1
JOIN route AS r2
ON (r1.num, r1.company) = (r2.num, r2.company)
JOIN stops AS s ON s.id = r2.stop
WHERE r1.stop = (SELECT id FROM stops WHERE name = 'Craiglockhart')
AND r1.company = 'LRT';
```
### 10.

#### Find the routes involving two buses that can go from Craiglockhart to Lochend.

#### Show the bus no. and company for the first bus, the name of the stop for the transfer, and the bus no. and company for the second bus.

```
SELECT r1.num, r1.company, s.name, r3.num, r3.company FROM route r1
JOIN route AS r2 ON (r1.num, r1.company) = (r2.num, r2.company)
JOIN route AS r3 ON (r2.stop) = (r3.stop)
JOIN route AS r4 ON (r3.num, r3.company) = (r4.num, r4.company)
JOIN stops AS s ON (s.id = r2.stop)
WHERE r1.stop = (SELECT stops.id FROM stops WHERE name = 'Craiglockhart')
AND r4.stop = (SELECT stops.id FROM stops WHERE name = 'Lochend')
ORDER BY r1.num, s.name, r3.num;
```