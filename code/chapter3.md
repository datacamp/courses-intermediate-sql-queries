# Sorting and Grouping
###### Sorting: ORDER BY
- ORDER BY (single)
- ORDER BY (multiple)
- ORDER BY DESC (single)
- ORDER BY DESC (multiple)

Get actors, sort by name.
```sql
SELECT name
FROM actors ORDER BY name;
```

Get actors, sort by name.
```sql
SELECT name
FROM actors
ORDER BY date_of_birth;
```

Get actors, sort by date_of_birth, then name.
```sql
SELECT name, date_of_birth
FROM actors
ORDER BY date_of_birth, name;
```

Get films filmed in 2000 or 2015, in order of release, and alphabetically.
```sql
SELECT title, release_year
FROM films
WHERE release_year IN (2000, 2015)
ORDER BY release_year, title;
```

Get films filmed between 2000 and 2015, in order of release, and alphabetically.
```sql
SELECT title, release_year
FROM films
WHERE release_year BETWEEN 2000 AND 2015
ORDER BY release_year, title;
```

###### Grouping: GROUP BY, HAVING
- GROUP BY (single)
- GROUP BY (multiple)
- GROUP BY then ORDER BY
- GROUP BY with COUNT
- GROUP BY with SUM
- GROUP BY with AVG
- GROUP BY with MIN
- GROUP BY with MAX
- HAVING

Get count of films made in each year.
```sql
SELECT COUNT(release_year), release_year
FROM films
GROUP BY release_year;
```

A PROPER GROUP BY ON MULTIPLE COLUMNS SHOULD GO HERE:
```sql
SELECT title, release_year box_office_millions
FROM films
GROUP BY title, release_year, box_office_millions;
```

Get count of films, group by release year then order by release year.
```sql
SELECT COUNT(title), release_year
FROM films
GROUP BY release_year
ORDER BY release_year;
```

Get count of films made in each year, ordered by count.
```sql
SELECT COUNT(release_year), release_year
FROM films
GROUP BY release_year
ORDER BY count;
```

Get lowest box office earnings per year.
```sql
SELECT release_year, MIN(box_office_millions)
FROM films
GROUP BY release_year
ORDER BY release_year;
```

Get highest box office earnings per year.
```sql
SELECT release_year, MAX(box_office_millions)
FROM films
GROUP BY release_year
ORDER BY release_year;
```

Get the total amount made by each distributor.
```sql
SELECT distributor, SUM(box_office_millions)
FROM films
GROUP BY distributor;
```

Get the total amount spent by each distributor.
```sql
SELECT distributor, SUM(box_office_millions)
FROM films
GROUP BY distributor;
```

Get the highest box office take per director.
```sql
SELECT director, MAX(box_office_millions)
FROM films
GROUP BY director;
```

Get the bottom ten lowest box office take per director.
```sql
SELECT director, MAX(box_office_millions)
FROM films
GROUP BY director
ORDER BY max DESC;
```

Get the average amount made by each distributor.
```sql
SELECT distributor, SUM(box_office_millions)
FROM films
GROUP BY distributor;
```

Get the average amount spent by each distributor.
```sql
SELECT distributor, SUM(box_office_millions)
FROM films
GROUP BY distributor;
```

** Note: here we have the problem of NULL being greater than 0 when using ORDER BY, i.e. not having enough data**
Get the total amount made by the bottom ten distributors.
```sql
SELECT distributor, sum(box_office_millions)
FROM films
GROUP BY distributor
ORDER BY sum
LIMIT 10;
```

**Note: here again we have the problem of the majority of NULL being greater than 0 when using ORDER BY, i.e. not having enough data**
Get the total amount made by the bottom ten distributors.
```sql
SELECT distributor, sum(budget_millions)
FROM films
GROUP BY distributor
ORDER BY sum
LIMIT 10;
```

Get average box office earnings per year.
```sql
SELECT release_year, AVG(box_office_millions)
FROM films
GROUP BY release_year
ORDER BY release_year;
```

**Note: Dates only go up to 2015**
Get lowest and highest box office earnings per year.
```sql
SELECT release_year, MIN(box_office_millions), MAX(box_office_millions)
FROM films
GROUP BY release_year
ORDER BY release_year DESC;
```

Get the average budget and average box office earnings for movies since 1990, but only if the average budget was greater than $60m in that year (Double check this).
```sql
SELECT release_year, AVG(budget_millions) AS avg_budget, AVG(box_office_millions) as avg_box_office
FROM films
WHERE release_year > 1990
GROUP BY release_year
HAVING AVG(budget_millions) > 60;
```

Get the name, average budget, average box office take of directors who have directed more than two films. Order by name, and get the top five. 
```sql
SELECT director, AVG(budget_millions) AS avg_budget, AVG(box_office_millions) as avg_box_office
FROM films
GROUP BY director
HAVING COUNT(title) > 2;
ORDER BY director
LIMIT 5;
```