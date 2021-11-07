---
title: Aggregate Functions
description: >-
  This chapter teaches you how to use aggregate functions to summarize data and
  gain useful insights. You'll also learn about arithmetic in SQL and how to use
  aliases to make your results more readable.
---

## Aggregate functions

```yaml
type: BulletExercise
key: b883e7079f
lang: sql
xp: 100
```

Often, you will want to perform some calculation on the data in a database. SQL provides a few functions, called *aggregate functions*, to help you out with this.

For example,

```
SELECT AVG(budget)
FROM films;
```

gives you the average value from the `budget` column of the `films` table. Similarly, the `MAX()` function returns the highest budget:

```
SELECT MAX(budget)
FROM films;
```

The `SUM()` function returns the result of adding up the numeric values in a column:

```
SELECT SUM(budget)
FROM films;
```

You can probably guess what the `MIN()` function does! Now it's your turn to try out some SQL functions.

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

***

```yaml
type: NormalExercise
key: 80fd462ae1
xp: 25
```

`@instructions`
Use the `SUM()` function to get the total duration of all films.

`@hint`
```
SELECT ___(___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT SUM(duration)
FROM films;
```

`@sct`
```{python}
custom_msg="Have you used `SUM(duration)`?"
Ex().check_correct(
    check_column('sum').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 7993b51268
xp: 25
```

`@instructions`
Get the average duration of all films.

`@hint`
```
SELECT ___(___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT AVG(duration)
FROM films;
```

`@sct`
```{python}
custom_msg="Have you used `AVG(duration)`?"
Ex().check_correct(
    check_column('avg').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: a03aeabbc6
xp: 25
```

`@instructions`
Get the duration of the shortest film.

`@hint`
```
SELECT ___(___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT MIN(duration)
FROM films;
```

`@sct`
```{python}
custom_msg="Have you used `MIN(duration)`?"
Ex().check_correct(
    check_column('min').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: fabbc619c6
xp: 25
```

`@instructions`
Get the duration of the longest film.

`@hint`
```
SELECT ___(___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT MAX(duration)
FROM films;
```

`@sct`
```{python}
custom_msg="Have you used `MAX(duration)`?"
Ex().check_correct(
    check_column('max').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast()
    )
)

Ex().success_msg("Sequelistic!")
```

---

## Aggregate functions practice

```yaml
type: BulletExercise
key: e60103b3f1
lang: sql
xp: 100
```

Good work. Aggregate functions are important to understand, so let's get some more practice!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

***

```yaml
type: NormalExercise
key: c8173b7d3e
xp: 25
```

`@instructions`
Use the `SUM()` function to get the total amount grossed by all films.

`@hint`
```
SELECT ___(___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT SUM(gross)
FROM films;
```

`@sct`
```{python}
custom_msg="Have you used `SUM(gross)`?"
Ex().check_correct(
    check_column('sum').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 24c0ab68ad
xp: 25
```

`@instructions`
Get the average amount grossed by all films.

`@hint`
```
SELECT ___(___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT AVG(gross)
FROM films;
```

`@sct`
```{python}
custom_msg="Have you used `AVG(gross)`?"
Ex().check_correct(
    check_column('avg').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 19838082cb
xp: 25
```

`@instructions`
Get the amount grossed by the worst performing film.

`@hint`
```
SELECT ___(___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT MIN(gross)
FROM films;
```

`@sct`
```{python}
custom_msg="Have you used `MIN(gross)`?"
Ex().check_correct(
    check_column('min').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: a49b98de42
xp: 25
```

`@instructions`
Get the amount grossed by the best performing film.

`@hint`
```
SELECT ___(___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT MAX(gross)
FROM films;
```

`@sct`
```{python}
custom_msg="Have you used `MAX(gross)`?"
Ex().check_correct(
    check_column('max').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast()
    )
)

Ex().success_msg("Well done! Don't forget about these functions. You'll find yourself using them over and over again to get a quick grasp of the data in a SQL database.")
```

---

## Combining aggregate functions with WHERE

```yaml
type: BulletExercise
key: b44bd43288
lang: sql
xp: 100
```

Aggregate functions can be combined with the `WHERE` clause to gain further insights from your data.

For example, to get the total budget of movies made in the year 2010 or later:

```
SELECT SUM(budget)
FROM films
WHERE release_year <= 2010;
```

Now it's your turn!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

***

```yaml
type: NormalExercise
key: b986f33a10
xp: 25
```

`@instructions`
Use the `SUM()` function to get the total amount grossed by all films made in the year 2000 or later.

`@hint`
```
SELECT ___(___)
FROM ___
WHERE ___ <= ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT SUM(gross)
FROM films
WHERE release_year <= 2000;
```

`@sct`
```{python}
custom_msg="Have you used `SUM(gross)`?"
Ex().check_correct(
    check_column('sum').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast(),
        check_edge('where_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 65e81175c5
xp: 25
```

`@instructions`
Get the average amount grossed by all films whose titles start with the letter 'A'.

`@hint`
```
SELECT ___(___)
FROM ___
WHERE ___ LIKE 'A%';
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT AVG(gross)
FROM films
where title LIKE 'A%';
```

`@sct`
```{python}
custom_msg="Have you used `AVG(gross)`?"
Ex().check_correct(
    check_column('avg').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast(),
        check_edge('where_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 3ca90a8536
xp: 25
```

`@instructions`
Get the amount grossed by the worst performing film in 1994.

`@hint`
```
SELECT ___(___)
FROM ___
WHERE ___ = ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT MIN(gross)
FROM films
WHERE release_year = 1994;
```

`@sct`
```{python}
custom_msg="Have you used `MIN(gross)`?"
Ex().check_correct(
    check_column('min').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast(),
        check_edge('where_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: d2e630e656
xp: 25
```

`@instructions`
Get the amount grossed by the best performing film between 2000 and 2012, inclusive.

`@hint`
```
SELECT ___(___)
FROM ___
WHERE ___ BETWEEN ___ AND ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT MAX(gross)
FROM films
WHERE release_year BETWEEN 2000 AND 2012;
```

`@sct`
```{python}
custom_msg="Have you used `MAX(gross)`?"
Ex().check_correct(
    check_column('max').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call', missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg),
        check_edge('from_clause').has_equal_ast(),
        check_edge('where_clause').has_equal_ast()
    )
)

Ex().success_msg("Nice. Can you see how SQL basically provides you a bunch of building blocks that you can combine in all kinds of ways? Hence the name: Structured Query Language.")
```

---

## A note on arithmetic

```yaml
type: MultipleChoiceExercise
key: 7b8b54b64d
lang: sql
xp: 50
skills:
  - 1
```

In addition to using aggregate functions, you can perform basic arithmetic with symbols like `+`, `-`, `*`, and `/`.

So, for example, this gives a result of `12`:

```
SELECT (4 * 3);
```

However, the following gives a result of `1`:

```
SELECT (4 / 3);
```

What's going on here?

SQL assumes that if you divide an integer by an integer, you want to get an integer back. So be careful when dividing!

If you want more precision when dividing, you can add decimal places to your numbers. For example,

```
SELECT (4.0 / 3.0) AS result;
```

gives you the result you would expect: `1.333`.

<hr>
What is the result of `SELECT (10 / 3);`?

`@possible_answers`
- 2.333
- 3.333
- 3
- 3.0

`@hint`
Run a query in the editor to the right.

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
```

`@sct`
```{python}
correct = 'Correct!'
icm = "Incorrect, read the exercise once more and try out the query in the editor!"
Ex().has_chosen(3, [icm, icm, correct, icm])
```

---

## It's AS simple AS aliasing

```yaml
type: BulletExercise
key: 9f4b026fe7
lang: sql
xp: 100
```

You may have noticed in the first exercise of this chapter that the column name of your result was just the name of the function you used. For example,

```
SELECT MAX(budget)
FROM films;
```

gives you a result with one column, named `max`. But what if you use two functions like this?

```
SELECT MAX(budget), MAX(duration)
FROM films;
```

Well, then you'd have two columns named `max`, which isn't very useful!

To avoid situations like this, SQL allows you to do something called _aliasing_. Aliasing simply means you assign a temporary name to something. To alias, you use the `AS` keyword, which you've already seen earlier in this course.

For example, in the above example we could use aliases to make the result clearer:

```
SELECT MAX(budget) AS max_budget,
       MAX(duration) AS max_duration
FROM films;
```

Aliases are helpful for making results more readable!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

***

```yaml
type: NormalExercise
key: ec33c2353b
xp: 35
```

`@instructions`
Get the title and net profit (the amount a film grossed, minus its budget) for all films. Alias the net profit as `net_profit`.

`@hint`
```
SELECT ___, ___ - ___ AS ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT title, gross - budget AS net_profit
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    multi(
        check_column('title').has_equal_value(),
        check_column('net_profit').has_equal_value()
    ),
    check_node('SelectStmt').multi(
        check_node('AliasExpr').has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 1351c6f6bb
xp: 35
```

`@instructions`
Get the title and duration in hours for all films. The duration is in minutes, so you'll need to divide by 60.0 to get the duration in hours. Alias the duration in hours as `duration_hours`.

`@hint`
```
SELECT ___, ___ / 60.0 AS ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT title, duration / 60.0 AS duration_hours
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    multi(
        check_column('title').has_equal_value(),
        check_column('duration_hours').has_equal_value()
    ),
    check_node('SelectStmt').multi(
        check_node('AliasExpr').has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 497f8d2a8a
xp: 30
```

`@instructions`
Get the average duration in hours for all films, aliased as `avg_duration_hours`.

`@hint`
```
SELECT ___(___) / 60.0 AS avg_duration_hours  
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT AVG(duration) / 60.0 AS avg_duration_hours  
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('avg_duration_hours').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('AliasExpr').has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )
)

Ex().success_msg("Boooom!")
```

---

## Even more aliasing

```yaml
type: BulletExercise
key: 7e3a93209c
lang: sql
xp: 100
```

Let's practice your newfound aliasing skills some more before moving on!


**Recall:** SQL assumes that if you divide an integer by an integer, you want to get an integer back. 

This means that the following will erroneously result in `400.0`:

```
SELECT 45 / 10 * 100.0;
```

This is because `45 / 10` evaluates to an integer (`4`), and not a decimal number like we would expect.

So when you're dividing make sure at least one of your numbers has a decimal place:

```
SELECT 45 * 100.0 / 10;
```

The above now gives the correct answer of `450.0` since the numerator (`45 * 100.0`) of the division is now a decimal!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'people'])
```

***

```yaml
type: NormalExercise
key: e14dc7c1a2
xp: 35
```

`@instructions`
Get the percentage of `people` who are no longer alive. Alias the result as `percentage_dead`. Remember to use `100.0` and not `100`!

`@hint`
```
SELECT ___(___) * 100.0 / ___(___) AS percentage_dead
FROM ___;
```

`@sample_code`
```{sql}
-- get the count(deathdate) and multiply by 100.0
-- then divide by count(*)
```

`@solution`
```{sql}
-- get the count(deathdate) and multiply by 100.0
-- then divide by count(*) 
SELECT COUNT(deathdate) * 100.0 / COUNT(*) AS percentage_dead
FROM people;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('percentage_dead').has_equal_value(),
    check_node('SelectStmt').multi(
        check_correct(
            check_node('AliasExpr').has_equal_ast(),
            has_code('100\.0', incorrect_msg="Make sure to use `100.0` to calculate the percentage!")
        ),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: c2bbd9a806
xp: 35
```

`@instructions`
Get the number of years between the newest film and oldest film. Alias the result as `difference`.

`@hint`
```
SELECT ___(___) - ___(___)
AS difference
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT MAX(release_year) - MIN(release_year)
AS difference
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('difference').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('AliasExpr').has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: f272486b68
xp: 30
```

`@instructions`
Get the number of decades the `films` table covers. Alias the result as `number_of_decades`. The top half of your fraction should be enclosed in parentheses.

`@hint`
```
SELECT (___(___) - ___(___)) / 10.0
AS number_of_decades
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT (MAX(release_year) - MIN(release_year)) / 10.0
AS number_of_decades
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('number_of_decades').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('AliasExpr').has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )
)

Ex().success_msg("We're at the end of chapter 3! In chapter 4, you will learn about sorting, grouping and joins. Head over there quickly!")
```
