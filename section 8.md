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