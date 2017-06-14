# Lesson 2 - Queries List
* Find the **Name** and **Birthday** of the **animals** whose **species** is Gorilla:
```mysql
SELECT name, birthdate FROM animals WHERE species = 'gorilla';
```

* Find the **names** of all the **animals** that are **not** gorillas **and not** named 'Max':
```mysql
SELECT name FROM animals WHERE NOT species = 'gorilla' AND NOT name = 'Max';
SELECT name FROM animals WHERE NOT (species = 'gorilla' OR name = 'Max');
SELECT name FROM animals WHERE species != 'gorilla' AND name != 'Max';
```

* Find all the **llamas** born **between** January 1, 1995 **and** December 31, 1998:
```mysql
SELECT name FROM animals WHERE species = 'llama' AND birthdate > '1995-01-01' AND birthdate < '1998-31-12';
```

* Find the **most used** name for animals:
```mysql
SELECT MAX(name) FROM animals;
```

* Find the **first 10** animals in the table:
```mysql
SELECT * FROM animals limit 10;
```

* Find **all** the orangutans **ordered by** birthdate:
```mysql
SELECT * FROM animals WHERE species = 'orangutan' ORDER BY birthdate;
```

* Find **all** the orangutans **ordered by** birthdate in **descending** order:
```mysql
SELECT name FROM animals WHERE species = 'orangutan' ORDER BY birthdate DESC;
```

* Find the name and birthdate of the **first 10** animals **after the** 20th:
```mysql
SELECT name, birthdate FROM animals ORDER BY name limit 10 offset 20;
```

* **For each** species of animals, find the **smallest** value of the birthdate column (the oldest animal birthday):
```mysql
SELECT species, MIN(birthdate) FROM animals GROUP BY species;
```

* Find the **first 5** elements of the **quantity** of names used for animals **ordered by** used times **descending**:
```mysql
SELECT name, COUNT(*) AS num FROM animals
GROUP BY name
ORDER BY num DESC
LIMIT 5;
```

* Write a query that returns **all** the species in the zoo, and **how many** animals of each species there are,
**sorted** with the **most populous** species **at the top**. The result should have **two columns**: species and
number. The animals table has columns (name, species, birthdate) for each individual.
```mysql
SELECT COUNT(*) AS num, species FROM animals
GROUP BY species
ORDER BY num DESC;
```

* Find the names and birthdates of **all** opossums:
```mysql
SELECT name, birthdate FROM animals WHERE species='opossum';
```

* Find the *names* of the *individual* animals *that* eat fish:
```mysql
SELECT name FROM animals JOIN diet ON animals.species = diet.species WHERE diet.food = 'fish';
SELECT name FROM animals, diet WHERE animals.species = diet.species AND diet.food = 'fish';
```

* Find the one food that is eaten by only one animal:
```mysql
SELECT food, COUNT(animals.name) AS num
FROM diet, animals
WHERE diet.species = animals.species
GROUP BY food
HAVING num = 1;
  
SELECT food, COUNT(animals.name) AS num
FROM diet JOIN animals 
ON diet.species = animals.species
GROUP BY food
HAVING num = 1;
```




## Lesson 2 Tables:
### Creation:
```mysql
CREATE TABLE animals (name text, species text, birthdate date);
CREATE TABLE diet (species text, food text); 
CREATE TABLE taxonomy (name text, species text, genus text, family text, t_order text); 
CREATE TABLE ordernames (t_order text, name text);
```

### Inserting:
```mysql
INSERT INTO animals VALUES('Hedgehog', 'opossum', '2017-06-13');
```
