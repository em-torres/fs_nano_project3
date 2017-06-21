# Lesson 4 - Queries List

* Returns a list of the players in the db whose weight is less than the average"
```mysql
SELECT name, weight FROM players WHERE weight < (SELECT avg(weight) AS av FROM players);
```
```mysql
SELECT name, weight
FROM players, (SELECT AVG(weight) AS av FROM players) as subq
WHERE weight < av;
```