---
title: Sorting and grouping
description: >-
  This chapter provides a brief introduction to sorting and grouping your
  results.
lessons:
  - nb_of_exercises: 5
    title: Sorting
  - nb_of_exercises: 4
    title: Grouping
  - nb_of_exercises: 3
    title: Bringing it all together
---

## ORDER BY

```yaml
type: PureMultipleChoiceExercise
key: 322af4938b
lang: sql
xp: 50
```

Congratulations on making it this far! You now know how to select and filter your results.

In this chapter you'll learn how to sort and group your results to gain further insight. Let's go!

In SQL, the `ORDER BY` keyword is used to sort results in ascending or descending order according to the values of one or more columns. 

By default `ORDER BY` will sort in ascending order. If you want to sort the results in descending order, you can use the `DESC` keyword. For example,

```
SELECT title
FROM films
ORDER BY release_year DESC;
```

gives you the titles of films sorted by release year, from newest to oldest.

<hr>
How do you think `ORDER BY` sorts a column of text values by default?

`@hint`
By default, `ORDER BY` sorts alphabetically, but in which direction?

`@possible_answers`
- [Alphabetically (A-Z)]
- Reverse alphabetically (Z-A)
- There's no natural ordering to text data
- By number of characters (fewest to most)

`@feedback`
- Correct!
- Incorrect. Although text values are ordered alphabetically, they don't go Z-A.
- Incorrect. Text values are ordered alphabetically.
- Incorrect. Text values are ordered alphabetically.

---

## Sorting single columns

```yaml
type: BulletExercise
key: a7b2964ba6
lang: sql
xp: 100
```

Now that you understand how `ORDER BY` works, give these exercises a go!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'people'])
```

***

```yaml
type: NormalExercise
key: e3a06cce15
xp: 35
```

`@instructions`
Get the names of people from the `people` table, sorted alphabetically.

`@hint`
```
SELECT ___
FROM ___
ORDER BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT name
FROM people
ORDER BY name;
```

`@sct`
```{python}
# Check whether the right column was included
Ex().check_column('name')

Ex().check_correct(
    # Check whether the name column is correct (taking into account order)
    check_column('name').has_equal_value(ordered=True),
    check_node('SelectStmt').multi(
        check_edge('from_clause').has_equal_ast(),
        check_edge('order_by_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 14a2792baa
xp: 35
```

`@instructions`
Get the names of people, sorted by birth date.

`@hint`
```
SELECT ___
FROM ___
ORDER BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT name
FROM people
ORDER BY birthdate;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('name').has_equal_value(ordered=True),
    check_node('SelectStmt').multi(
        check_edge('from_clause').has_equal_ast(),
        check_edge('order_by_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 6cfeca71b1
xp: 30
```

`@instructions`
Get the birth date and name for every person, in order of when they were born.

`@hint`
```
SELECT ___, ___
FROM ___
ORDER BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT birthdate, name
FROM people
ORDER BY birthdate;
```

`@sct`
```{python}
# Check whether the right columns are included
Ex().check_all_columns()

# Check whether the order is correct
Ex().check_correct(
    check_all_columns().has_equal_value(ordered=True),
    check_node('SelectStmt').multi(
        check_edge('from_clause').has_equal_ast(),
        check_edge('order_by_clause').has_equal_ast()
    )
)
```

---

## Sorting single columns (2)

```yaml
type: BulletExercise
key: 357ec9bc3d
lang: sql
xp: 100
```

Let's get some more practice with `ORDER BY`!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'people'])
```

***

```yaml
type: NormalExercise
key: e2702b5933
xp: 35
```

`@instructions`
Get the title of films released in 2000 or 2012, in the order they were released.

`@hint`
```
SELECT ___
FROM ___
WHERE ___ IN (___, ___)
ORDER BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT title
FROM films
WHERE release_year IN (2000, 2012)
ORDER BY release_year;
```

`@sct`
```{python}
# First check if where statement was coded correctly
Ex().check_correct(
    has_nrows(),
    check_node('SelectStmt').multi(
        check_edge('from_clause').has_equal_ast(),
        check_edge('where_clause').has_equal_ast()
    )
)

# Next, check if right columns were included in the right order:
Ex().check_column('title')
Ex().check_correct(
    check_column('title').has_equal_value(ordered=True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)
```

***

```yaml
type: NormalExercise
key: 5c84507976
xp: 35
```

`@instructions`
Get all details for all films except those released in 2015 and order them by duration.

`@hint`
```{sql}
SELECT ___
FROM ___
WHERE ___ <> ___
ORDER BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT *
FROM films
WHERE release_year <> 2015
ORDER BY duration;
```

`@sct`
```{python}
# First check if where statement was coded correctly
Ex().check_correct(
    has_nrows(),
    check_node('SelectStmt').multi(
        check_edge('from_clause').has_equal_ast(),
        check_edge('where_clause').has_equal_ast()
    )
)

# Next, check if all columns included
Ex().check_correct(
    check_all_columns(),
    check_node('SelectStmt').check_node('Star', missing_msg="Are you using `SELECT *` to select _all_ columns?")
)

# Finally, check if order is correct
Ex().check_correct(
    check_all_columns().has_equal_value(ordered = True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)
```

***

```yaml
type: NormalExercise
key: 6359addbf8
xp: 30
```

`@instructions`
Get the title and gross earnings for movies which begin with the letter 'M' and order the results alphabetically.

`@hint`
```{sql}
SELECT ___, ___
FROM ___
WHERE ___ LIKE ___
ORDER BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT title, gross
FROM films
WHERE title LIKE 'M%'
ORDER BY title;
```

`@sct`
```{python}
# First check if where statement was coded correctly
Ex().check_correct(
    has_nrows(),
    check_node('SelectStmt').multi(
        check_edge('from_clause').has_equal_ast(),
        check_edge('where_clause').has_equal_ast()
    )
)

# Next, check if all columns included
Ex().check_all_columns()

# Finally, check if order is correct
Ex().check_correct(
    check_all_columns().has_equal_value(ordered = True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)

Ex().success_msg("Can you feel the SQL power dawn on you?!")
```

---

## Sorting single columns (DESC)

```yaml
type: BulletExercise
key: a7b2964ba7
lang: sql
xp: 100
```

To order results in _descending_ order, you can put the keyword `DESC` after your `ORDER BY`. For example, to get all the names in the `people` table, in reverse alphabetical order:

```
SELECT name
FROM people
ORDER BY name DESC;
```

Now practice using `ORDER BY` with `DESC` to sort single columns in descending order!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'reviews'])
```

`@sample_code`
```{sql}

```

***

```yaml
type: NormalExercise
key: 1ed651456d
xp: 35
```

`@instructions`
Get the IMDB score and film ID for every film from the reviews table, sorted from highest to lowest score.

`@hint`
```
SELECT ___, ___
FROM ___
ORDER BY ___ DESC;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT imdb_score, film_id
FROM reviews
ORDER BY imdb_score DESC;
```

`@sct`
```{python}
# Check if all required columns included
Ex().check_all_columns()

# Check if order is correct
Ex().check_correct(
    check_all_columns().has_equal_value(ordered = True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)
```

***

```yaml
type: NormalExercise
key: 3629dd5dcd
xp: 35
```

`@instructions`
Get the title for every film, in reverse order.

`@hint`
```
SELECT ___
FROM ___
ORDER BY ___ ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT title
FROM films
ORDER BY title DESC;
```

`@sct`
```{python}
# Check if all required columns included
Ex().check_column('title')

# Check if order is correct
Ex().check_correct(
    check_column('title').has_equal_value(ordered = True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)
```

***

```yaml
type: NormalExercise
key: ddcb2dd3ad
xp: 30
```

`@instructions`
Get the title and duration for every film, in order of longest duration to shortest.

`@hint`
```
SELECT ___, ___
FROM ___
ORDER BY ___ ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT title, duration
FROM films
ORDER BY duration DESC;
```

`@sct`
```{python}
# Check if all required columns included
Ex().check_all_columns()

# Check if order is correct
Ex().check_correct(
    check_all_columns().has_equal_value(ordered=True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)

Ex().success_msg("Nice. Let's explore how you can sort multiple columns!")
```

---

## Sorting multiple columns

```yaml
type: BulletExercise
key: b2a52993bc
lang: sql
xp: 100
```

`ORDER BY` can also be used to sort on multiple columns. It will sort by the first column specified, then sort by the next, then the next, and so on. For example,

```
SELECT birthdate, name
FROM people
ORDER BY birthdate, name;
```

sorts on birth dates first (oldest to newest) and then sorts on the names in alphabetical order. **The order of columns is important!**

Try using `ORDER BY` to sort multiple columns! Remember, to specify multiple columns you separate the column names with a comma.

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'people'])
```

***

```yaml
type: NormalExercise
key: 9ec6e8ae72
xp: 25
```

`@instructions`
Get the birth date and name of people in the `people` table, in order of when they were born and alphabetically by name.

`@hint`
```
SELECT ___, ___
FROM ___
ORDER BY ___, ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT birthdate, name
FROM people
ORDER BY birthdate, name;
```

`@sct`
```{python}
# Check if all required columns included
Ex().check_all_columns()

# Check if order is correct
Ex().check_correct(
    check_all_columns().has_equal_value(ordered=True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)
```

***

```yaml
type: NormalExercise
key: 3460b2f14b
xp: 25
```

`@instructions`
Get the release year, duration, and title of films ordered by their release year and duration.

`@hint`
```
SELECT ___, ___, ___
FROM ___
ORDER BY ___, ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT release_year, duration, title
FROM films
ORDER BY release_year, duration;
```

`@sct`
```{python}
# Check if all required columns included
Ex().check_all_columns()

# Check if order is correct
Ex().check_correct(
    check_all_columns().has_equal_value(ordered=True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)
```

***

```yaml
type: NormalExercise
key: c03517c2b9
xp: 25
```

`@instructions`
Get certifications, release years, and titles of films ordered by certification (alphabetically) and release year.

`@hint`
```
SELECT ___, ___, ___
FROM ___
ORDER BY ___, ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT certification, release_year, title
FROM films
ORDER BY certification, release_year;
```

`@sct`
```{python}
# Check if all required columns included
Ex().check_all_columns()

# Check if order is correct
Ex().check_correct(
    check_all_columns().has_equal_value(ordered=True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)
```

***

```yaml
type: NormalExercise
key: f0ade213ff
xp: 25
```

`@instructions`
Get the names and birthdates of people ordered by name and birth date.

`@hint`
```
SELECT ___, ___
FROM ___
ORDER BY ___, ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT name, birthdate
FROM people
ORDER BY name, birthdate;
```

`@sct`
```{python}
# Check if all required columns included
Ex().check_all_columns()

# Check if order is correct
Ex().check_correct(
    check_all_columns().has_equal_value(ordered=True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)

Ex().success_msg("Well done. Notice how the second column you order on only steps in when the first column is not decisive to tell the order. The second column acts as a tie breaker.")
```

---

## GROUP BY

```yaml
type: PureMultipleChoiceExercise
key: 81987a99cf
lang: sql
xp: 50
```

Now you know how to sort results! Often you'll need to aggregate results. For example, you might want to count the number of male and female employees in your company. Here, what you want is to group all the males together and count them, and group all the females together and count them. In SQL, `GROUP BY` allows you to group a result by one or more columns, like so:

```
SELECT sex, count(*)
FROM employees
GROUP BY sex;
```

This might give, for example:

```out
| sex    | count |
|--------|-------|
| male   | 15    |
| female | 19    |

```
<br>
Commonly, `GROUP BY` is used with _aggregate functions_ like `COUNT()` or `MAX()`. Note that `GROUP BY` always goes after the `FROM` clause!

<hr>
What is `GROUP BY` used for?

`@hint`
You use `GROUP BY` when you want to compute results within groups.

`@possible_answers`
- Performing operations by column
- Performing operations all at once
- Performing operations in a particular order
- [Performing operations by group]

`@feedback`
- Incorrect. While `GROUP BY` does sort by column, we could just use `ORDER BY` for this.
- Incorrect.
- Incorrect. While `GROUP BY` does sort results, it's not designed to control order of operations.
- Correct! `GROUP BY` is for performing operations within groups.

---

## GROUP BY practice

```yaml
type: BulletExercise
key: 98e30a6131
lang: sql
xp: 100
```

As you've just seen, combining aggregate functions with `GROUP BY` can yield some powerful results!

A word of warning: SQL will return an error if you try to `SELECT` a field that is not in your `GROUP BY` clause without using it to calculate some kind of value about the entire group.

Note that you can combine `GROUP BY` with `ORDER BY` to group your results, calculate something about them, and then order your results. For example,

```
SELECT sex, count(*)
FROM employees
GROUP BY sex
ORDER BY count DESC;
```

might return something like

```out
| sex    | count |
|--------|-------|
| female | 19    |
| male   | 15    |
```

<br>
because there are more females at our company than males. Note also that `ORDER BY` always goes after `GROUP BY`. Let's try some exercises!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'reviews'])
```

***

```yaml
type: NormalExercise
key: 0b29eb4ff3
xp: 25
```

`@instructions`
Get the release year and count of films released in each year.

`@hint`
```
SELECT ___, ___(___)
FROM ___
GROUP BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT release_year, COUNT(*)
FROM films
GROUP BY release_year;
```

`@sct`
```{python}
groupby_msg = "Make sure to include a `GROUP BY` statement!"
custom_msg = "Are you using `COUNT(*)`?"
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        # If grouping is not done, it will not work in the first place
        check_edge('group_by_clause', missing_msg=groupby_msg).has_equal_ast(),
        check_node("Call", missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg)
    )
)
```

***

```yaml
type: NormalExercise
key: ebee043890
xp: 25
```

`@instructions`
Get the release year and average duration of all films, grouped by release year.

`@hint`
```
SELECT ___, ___(___)
FROM ___
GROUP BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT release_year, AVG(duration)
FROM films
GROUP BY release_year;
```

`@sct`
```{python}
groupby_msg = "Make sure to include a `GROUP BY` statement!"
custom_msg = "Are you using `AVG(duration)`?"
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        # If grouping is not done, it will not work in the first place
        check_edge('group_by_clause', missing_msg=groupby_msg).has_equal_ast(),
        # If grouping is okay, it makes sense to look at the Call part.
        check_node("Call", missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg)
    )
)
```

***

```yaml
type: NormalExercise
key: b4341b8451
xp: 25
```

`@instructions`
Get the release year and largest budget for all films, grouped by release year.

`@hint`
```
SELECT ___, ___(___)
FROM ___
GROUP BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT release_year, MAX(budget)
FROM films
GROUP BY release_year;
```

`@sct`
```{python}
groupby_msg = "Make sure to include a `GROUP BY` statement!"
custom_msg = "Are you using `MAX(budget)`?"
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        # If grouping is not done, it will not work in the first place
        check_edge('group_by_clause', missing_msg=groupby_msg).has_equal_ast(),
        # If grouping is okay, it makes sense to look at the Call part.
        check_node("Call", missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg)
    )
)
```

***

```yaml
type: NormalExercise
key: 66d0c5198a
xp: 25
```

`@instructions`
Get the IMDB score and count of film reviews grouped by IMDB score in the `reviews` table.

`@hint`
```
SELECT ___, ___(___)
FROM ___
GROUP BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT imdb_score, COUNT(*)
FROM reviews
GROUP BY imdb_score;
```

`@sct`
```{python}
groupby_msg = "Make sure to include a `GROUP BY` statement!"
custom_msg = "Are you using `COUNT(*)`?"
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        # If grouping is not done, it will not work in the first place
        check_edge('group_by_clause', missing_msg=groupby_msg).has_equal_ast(),
        # If grouping is okay, it makes sense to look at the Call part.
        check_node("Call", missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg)
    )
)

Ex().success_msg("Now that you've accustomed yourself with `GROUP BY`, let's throw it in the mix with other SQL constructs you already know!")
```

---

## GROUP BY practice (2)

```yaml
type: BulletExercise
key: 38a7c62434
lang: sql
xp: 100
```

Now practice your new skills by combining `GROUP BY` and `ORDER BY` with some more aggregate functions!

Make sure to always put the `ORDER BY` clause at the end of your query. You can't sort values that you haven't calculated yet!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

***

```yaml
type: NormalExercise
key: 53ad6da98c
xp: 20
```

`@instructions`
Get the release year and lowest gross earnings per release year.

`@hint`
```
SELECT ___, ___(___)
FROM ___
GROUP BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT release_year, MIN(gross)
FROM films
GROUP BY release_year;
```

`@sct`
```{python}
groupby_msg = "Make sure to include a `GROUP BY` statement!"
custom_msg = "Are you using `MIN(gross)`?"
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        # If grouping is not done, it will not work in the first place
        check_edge('group_by_clause', missing_msg=groupby_msg).has_equal_ast(),
        # If grouping is okay, it makes sense to look at the Call part.
        check_node("Call", missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg)
    )
)
```

***

```yaml
type: NormalExercise
key: cff5924de5
xp: 20
```

`@instructions`
Get the language and total gross amount films in each language made.

`@hint`
```
SELECT ___, ___(___)
FROM ___
GROUP BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT language, SUM(gross)
FROM films
GROUP BY language;
```

`@sct`
```{python}
groupby_msg = "Make sure to include a `GROUP BY` statement!"
custom_msg = "Are you using `SUM(gross)`?"
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        # If grouping is not done, it will not work in the first place
        check_edge('group_by_clause', missing_msg=groupby_msg).has_equal_ast(),
        # If grouping is okay, it makes sense to look at the Call part.
        check_node("Call", missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg)
    )
)
```

***

```yaml
type: NormalExercise
key: 83944ff64f
xp: 20
```

`@instructions`
Get the country and total budget spent making movies in each country.

`@hint`
```
SELECT ___, ___(___)
FROM ___
GROUP BY ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT country, SUM(budget)
FROM films
GROUP BY country;
```

`@sct`
```{python}
groupby_msg = "Make sure to include a `GROUP BY` statement!"
custom_msg = "Are you using `SUM(budget)`?"
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        # If grouping is not done, it will not work in the first place
        check_edge('group_by_clause', missing_msg=groupby_msg).has_equal_ast(),
        # If grouping is okay, it makes sense to look at the Call part.
        check_node("Call", missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg)
    )
)
```

***

```yaml
type: NormalExercise
key: eac5f722a5
xp: 20
```

`@instructions`
Get the release year, country, and highest budget spent making a film for each year, for each country. Sort your results by release year and country.

`@hint`
```
SELECT ___, ___, ___(___)
FROM ___
GROUP BY ___, ___
ORDER BY ___, ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT release_year, country, MAX(budget)
FROM films
GROUP BY release_year, country
ORDER BY release_year, country;
```

`@sct`
```{python}
groupby_msg = "Make sure to include a `GROUP BY` statement!"
custom_msg = "Are you using `MAX(budget)`?"
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        # If grouping is not done, it will not work in the first place
        check_edge('group_by_clause', missing_msg=groupby_msg).has_equal_ast(),
        # If grouping is okay, it makes sense to look at the Call part.
        check_node("Call", missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg)
    )
)

# Verify the ordering.
Ex().check_correct(
    check_all_columns().has_equal_value(ordered=True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)
```

***

```yaml
type: NormalExercise
key: 48461bd4d3
xp: 20
```

`@instructions`
Get the country, release year, and lowest amount grossed per release year per country. Order your results by country and release year.

`@hint`
```
SELECT ___, ___, ___(___)
FROM films
GROUP BY country, release_year
ORDER BY ___, ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT country, release_year, MIN(gross)
FROM films
GROUP BY country, release_year
ORDER BY country, release_year;
```

`@sct`
```{python}
groupby_msg = "Make sure to include a `GROUP BY` statement!"
custom_msg = "Are you using `MIN(gross)`?"
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        # If grouping is not done, it will not work in the first place
        check_edge('group_by_clause', missing_msg=groupby_msg).has_equal_ast(),
        # If grouping is okay, it makes sense to look at the Call part.
        check_node("Call", missing_msg=custom_msg).has_equal_ast(incorrect_msg=custom_msg)
    )
)

# Verify the ordering.
Ex().check_correct(
    check_all_columns().has_equal_value(ordered=True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)

Ex().success_msg("Off to the next statement!")
```

---

## HAVING a great time

```yaml
type: MultipleChoiceExercise
key: a391d35885
lang: sql
xp: 50
```

In SQL, aggregate functions can't be used in `WHERE` clauses. For example, the following query is invalid:

```
SELECT release_year
FROM films
GROUP BY release_year
WHERE COUNT(title) > 10;
```

This means that if you want to filter based on the result of an aggregate function, you need another way! That's where the `HAVING` clause comes in. For example,

```
SELECT release_year
FROM films
GROUP BY release_year
HAVING COUNT(title) > 10;
```

shows only those years in which more than 10 films were released.

<hr>
In how many different years were more than 200 movies released?

`@possible_answers`
- 2
- 13
- 44
- 63

`@hint`
Replace 10 with 200 in the query above and run it in the editor.

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

`@sct`
```{python}
msg1 = "It's more than that! Copy and paste the code from the example query, make a small modification, and run it to answer the question!"
msg2 = "That's correct! We're nearing the end of the course, so it's time to combine everything that you've learned and answer some interesting questions!"
msg3 = '44 is the number of different years in which more than 10 movies were released. Make sure to answer the same question but for _200_ movies.'
msg4 = "Not that much! Copy and paste the code from the example query, make a small modification, and run it to answer the question!"
Ex().has_chosen(2, [msg1, msg2, msg3, msg4])
```

---

## All together now

```yaml
type: TabExercise
key: f7dcb9e122
lang: sql
xp: 100
```

Time to practice using `ORDER BY`, `GROUP BY` and `HAVING` together.

Now you're going to write a query that returns the average budget and average gross earnings for films in each year after 1990, if the average budget is greater than $60 million.

This is going to be a big query, but you can handle it!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

***

```yaml
type: NormalExercise
key: a141cd669f
xp: 16
```

`@instructions`
Get the release year, budget and gross earnings for each film in the `films` table.

`@hint`
```
SELECT ___, ___, ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT release_year, budget, gross
FROM films;
```

`@sct`
```{python}
Ex().check_all_columns(allow_extra=False).has_equal_value()
```

***

```yaml
type: NormalExercise
key: d80bd57b13
xp: 16
```

`@instructions`
Modify your query so that only records with a `release_year` after 1990 are included.

`@hint`
```
SELECT ___, ___, ___
FROM ___
WHERE ___ > ___;
```

`@sample_code`
```{sql}
SELECT release_year, budget, gross
FROM films;
```

`@solution`
```{sql}
SELECT release_year, budget, gross
FROM films
WHERE release_year > 1990;
```

`@sct`
```{python}
# First check that WHERE was coded correctly
Ex().check_correct(
    has_nrows(),
    check_node('SelectStmt').check_edge('where_clause').has_equal_ast()
)

# Check whether the right columns where selected
Ex().check_all_columns(allow_extra=False).has_equal_value()
```

***

```yaml
type: NormalExercise
key: 2d5e6bd8cf
xp: 17
```

`@instructions`
Remove the budget and gross columns, and group your results by release year.

`@hint`
```
SELECT ___
FROM ___
WHERE ___ > ___
GROUP BY ___;
```

`@sample_code`
```{sql}
SELECT release_year
FROM films
WHERE release_year > 1990;
```

`@solution`
```{sql}
SELECT release_year
FROM films
WHERE release_year > 1990
GROUP BY release_year;
```

`@sct`
```{python}
# First check that WHERE and GROUP BY was coded correctly
Ex().check_correct(
    has_nrows(),
    check_node('SelectStmt').multi(
        check_edge('where_clause').has_equal_ast(),
        check_edge('group_by_clause').has_equal_ast()
    )
)

# Check whether the right columns where selected
Ex().check_all_columns(allow_extra=False).has_equal_value()
```

***

```yaml
type: NormalExercise
key: ee92d8cbaa
xp: 17
```

`@instructions`
Modify your query to include the average budget and average gross earnings for the results you have so far. Alias the average budget as `avg_budget`; alias the average gross earnings as `avg_gross`.

`@hint`
```
SELECT ___, ___(___) AS avg_budget, 
       AVG(gross) AS avg_gross
FROM ___
WHERE ___ > ___
GROUP BY ___;
```

`@sample_code`
```{sql}
SELECT release_year,
FROM films
WHERE release_year > 1990
GROUP BY release_year;
```

`@solution`
```{sql}
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year;
```

`@sct`
```{python}
# First check that WHERE and GROUP BY was coded correctly
Ex().check_correct(
    has_nrows(),
    check_node('SelectStmt').multi(
        check_edge('where_clause').has_equal_ast(),
        check_edge('group_by_clause').has_equal_ast()
    )
)

# Check whether release_year is correct
Ex().check_column('release_year').has_equal_value()

# Check whether avg_budget is included and calculated properly
Ex().check_column('avg_budget')
Ex().check_correct(
    check_column('avg_budget').has_equal_value(),
    check_node('SelectStmt').check_node('AliasExpr', 0).has_equal_ast()
)

# Check whether avg_gross is included and calculated properly
Ex().check_column('avg_gross')
Ex().check_correct(
    check_column('avg_gross').has_equal_value(),
    check_node('SelectStmt').check_node('AliasExpr', 1).has_equal_ast()
)
```

***

```yaml
type: NormalExercise
key: ce0f248734
xp: 17
```

`@instructions`
Modify your query so that only years with an average budget of greater than $60 million are included.

`@hint`
```
SELECT ___, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM ___
WHERE ___ > ___
GROUP BY ___
HAVING AVG(___) > 60000000;
```

`@sample_code`
```{sql}
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year;
```

`@solution`
```{sql}
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year
HAVING AVG(budget) > 60000000;
```

`@sct`
```{python}
# Check if all columns are still there
msg = "Don't include any additional columns: stick with `release_year`, `avg_budget`, and `avg_gross`."
Ex().check_column('release_year', missing_msg=msg)
Ex().check_column('avg_budget', missing_msg=msg)
Ex().check_column('avg_gross', missing_msg=msg)
Ex().check_all_columns(allow_extra=False)

# Then check if the contents are correct
Ex().check_correct(
    check_all_columns(allow_extra=False).has_equal_value(),
    check_node('SelectStmt').multi(
        check_edge('where_clause').has_equal_ast(),
        check_edge('group_by_clause').has_equal_ast(),
        check_edge('having_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 7b3afeed2f
xp: 17
```

`@instructions`
Finally, modify your query to order the results from highest average gross earnings to lowest.

`@hint`
```
SELECT ___, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM ___
WHERE ___ > ___
GROUP BY ___
HAVING AVG(___) > 60000000
ORDER BY ___ DESC;
```

`@sample_code`
```{sql}
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year
HAVING AVG(budget) > 60000000;
```

`@solution`
```{sql}
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year
HAVING AVG(budget) > 60000000
ORDER BY avg_gross DESC;
```

`@sct`
```{python}
# Check if all columns are still there
msg = "Don't include any additional columns: stick with `release_year`, `avg_budget`, and `avg_gross`."
Ex().check_column('release_year', missing_msg=msg)
Ex().check_column('avg_budget', missing_msg=msg)
Ex().check_column('avg_gross', missing_msg=msg)
Ex().check_all_columns(allow_extra=False)

# Then check if the contents are correct
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        check_edge('where_clause').has_equal_ast(),
        check_edge('group_by_clause').has_equal_ast(),
        check_edge('having_clause').has_equal_ast()
    )
)

# Check if it's the right order
Ex().check_correct(
    check_all_columns().has_equal_value(ordered=True),
    check_node('SelectStmt').check_edge('order_by_clause').has_equal_ast()
)

Ex().success_msg("Wooooow! Let's do another one!")
```

---

## All together now (2)

```yaml
type: NormalExercise
key: 0bbc6da34d
lang: sql
xp: 100
skills:
  - 1
```

Great work! Now try another large query. This time, all in one go!

Remember, if you only want to return a certain number of results, you can use the `LIMIT` keyword to limit the number of rows returned

`@instructions`
Get the country, average budget, and average gross take of countries that have made more than 10 films. Order the result by country name, and limit the number of results displayed to 5. You should alias the averages as `avg_budget` and `avg_gross` respectively.

`@hint`
```
SELECT ___, AVG(budget) AS avg_budget, 
       ___(gross) AS avg_gross
FROM films
GROUP BY ___
HAVING COUNT(title) > 10
ORDER BY ___
LIMIT 5;
```

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

`@sample_code`
```{sql}
-- select country, average budget, 
--     and average gross

-- from the films table

-- group by country 

-- where the country has more than 10 titles

-- order by country

-- limit to only show 5 results
```

`@solution`
```{sql}
-- select country, average budget, 
-- and average gross
SELECT country, AVG(budget) AS avg_budget, 
       AVG(gross) AS avg_gross
-- from the films table
FROM films
-- group by country 
GROUP BY country
-- where the country has more than 10 titles
HAVING COUNT(title) > 10
-- order by country
ORDER BY country
-- limit to only show 5 results
LIMIT 5;
```

`@sct`
```{python}
Ex().check_correct(
    # If end result is ok, all fine all good.
    check_all_columns(allow_extra=False).has_equal_value(ordered=True),
    # If not, let's dive deeper
    multi(
        # First look at the elements that influence the number of records
        check_correct(
            has_nrows(),
            check_node('SelectStmt').multi(
                check_edge('from_clause').has_equal_ast(),
                check_edge('group_by_clause').has_equal_ast(),
                check_edge('having_clause').has_equal_ast(),
                check_edge('limit_clause').has_equal_ast()
            )
        ),
        # If that is good, look at the separate columns and how they are calculated
        check_column('country').has_equal_value(),
        check_column('avg_budget'),
        check_correct(
            check_column('avg_budget').has_equal_value(),
            check_node('SelectStmt').check_node('AliasExpr', 0).has_equal_ast()
        ),
        check_correct(
            check_column('avg_gross').has_equal_value(),
            check_node('SelectStmt').check_node('AliasExpr', 1).has_equal_ast()
        ),
        check_node('SelectStmt').check_edge('order_by_clause')
    )
)

Ex().success_msg("Superb work on a selection saga! `SELECT` queries can get rather long, but breaking them down into individual clauses makes them easier to write.")
```

---

## A taste of things to come

```yaml
type: TabExercise
key: d101be707a
lang: sql
xp: 100
```

Congrats on making it to the end of the course! By now you should have a good understanding of the basics of SQL.

There's one more concept we're going to introduce. You may have noticed that all your results so far have been from just one table, e.g., `films` or `people`.

In the real world however, you will often want to query multiple tables. For example, what if you want to see the IMDB score for a particular movie?

In this case, you'd want to get the ID of the movie from the `films` table and then use it to get IMDB information from the `reviews` table. In SQL, this concept is known as a **join**, and a basic join is shown in the editor to the right.

The query in the editor gets the IMDB score for the film _To Kill a Mockingbird_! Cool right?

As you can see, joins are incredibly useful and important to understand for anyone using SQL.

We have a whole follow-up course dedicated to them called <a href="https://learn.datacamp.com/courses/joining-data-in-postgresql">Joining Data in SQL</a> for you to hone your database skills further!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'reviews'])
```

***

```yaml
type: NormalExercise
key: 7c4fc7a484
xp: 50
```

`@instructions`
Submit the code in the editor and inspect the results.

`@hint`
Submit the code in the editor!

`@sample_code`
```{sql}
SELECT title, imdb_score
FROM films
JOIN reviews
ON films.id = reviews.film_id
WHERE title = 'To Kill a Mockingbird';
```

`@solution`
```{sql}
SELECT title, imdb_score
FROM films
JOIN reviews
ON films.id = reviews.film_id
WHERE title = 'To Kill a Mockingbird';
```

`@sct`
```{python}
Ex().check_all_columns(allow_extra=False).has_equal_value()
```

***

```yaml
type: MultipleChoiceExercise
key: fc288db979
xp: 50
```

`@question`
Here is the result of your last query that joined the `films` and `reviews` tables:
```out
| title                 | imdb_score |
|-----------------------|------------|
| To Kill a Mockingbird | 8.4        |
```
What is the IMDB score for the film _To Kill a Mockingbird_?

`@sample_code`
```{sql}

```

`@possible_answers`
- 8.1
- 8.4
- 7.7
- 9.3

`@hint`
Look at the query result in the instructions!

`@sct`
```{python}
icm = 'Have another look at the result of the query you just submitted. The answer is right there!'
correct = 'Correct! To continue your SQL journey and discover the power of joins, take the Joining Data with SQL course!'
Ex().has_chosen(2,[icm, correct, icm, icm])
```
