---
title: Selecting columns
description: >-
  This chapter provides a brief introduction to working with relational
  databases. You'll learn about their structure, how to talk about them using
  database lingo, and how to begin an analysis by using simple SQL commands to
  select and summarize columns from database tables.

--- type:VideoExercise lang:sql xp:50 skills:1 key:dcdbb24914
## Welcome to the course!

*** =projector_key
f05d06ad7807cf476fdb5f674174c9d5

--- type:TabExercise lang:sql xp:100 skills:1 key:0cbd791cc8
## Onboarding

If you've used DataCamp to learn [R](https://www.datacamp.com/courses/free-introduction-to-r) or [Python](https://www.datacamp.com/courses/intro-to-python-for-data-science), you'll be familiar with the interface.

For SQL however, we're introducing some new features.

In the real world you will often need to incrementally build up your queries. To reflect this, we're introducing *tab exercises*. Check it out below!

*** =pre_exercise_code
```{python}
connect('postgresql', 'films')
```

*** =sample_code
```{sql}
-- Try running me!
SELECT 'Welcome to the course!'
AS welcome_column;
```

*** =type1:NormalExercise
*** =key1: 0e1942875c
*** =xp1: 20

*** =instructions1
Notice the **query result** tab in the bottom right corner of your screen. This is where the results of your SQL queries will be displayed.

Run the query in the editor and check out the results in the **query result** tab!

*** =hint1
Run the code in the editor!

*** =solution1
```{sql}
-- Try running me!
SELECT 'Welcome to the course!'
AS welcome_column;
```

*** =sct1
```{python}
Ex().test_has_columns()
Ex().test_error()
Ex().test_student_typed('SELECT', msg='You need to add `SELECT` at the start of line 2!', fixed=True)
```

*** =type2:MultipleChoiceExercise
*** =key2: 97d9538682
*** =xp2: 20

*** =question2
Good work!

For this course, you'll be using a database containing information on almost 5000 films. To the right, underneath the editor, you can see the tables in this database by clicking through the tabs.

From looking at the tables, who is the first person listed in the `people` table?

*** =possible_answers2
- Kanye West
- Biggy Smalls
- 50 Cent
- Jay Z

*** =hint2
Look at the `people` tab under the editor!

*** =sct2
```{python}
msg1 = 'Nope, look at the `people` table!'
correct = 'Correct!'

Ex().test_mc(3,[msg1, msg1, correct, msg1])
```

--- type:BulletExercise lang:sql xp:100 skills:1 key:f76443aff1
## Onboarding (2)

Another new feature we're introducing is *bullet exercises*, which allow you to easily practice a new concept through repetition. Check it out below!

*** =pre_exercise_code
```{python}
connect('postgresql', 'films')
```

*** =sample_code
```{sql}
SELECT 'SQL'
AS result;
```

*** =type1:NormalExercise
*** =key1: 157ee8d1ad
*** =xp1: 20

*** =instructions1
Submit the query in the editor! Don't worry, you'll learn how it works soon.

*** =hint1
Submit the query!

*** =solution1
```{sql}
SELECT 'SQL'
AS result;
```

*** =sct1
```{sql}
Ex().test_error()

Ex().test_student_typed('SQL', msg="Don't modify the query!", fixed=True)

Ex().test_has_columns()
Ex().check_result()

```

*** =type2:NormalExercise
*** =key2: 764f82129d
*** =xp2: 20

*** =instructions2
Now change 'SQL' to 'SQL is' and click Submit!

*** =hint2
Change the code and submit the query!

*** =solution2
```{sql}
SELECT 'SQL is'
AS result;
```

*** =sct2
```{sql}
Ex().test_error()

Ex().test_student_typed('SQL is', msg="Did you change the query correctly?", fixed=True)

Ex().test_has_columns()
Ex().check_result()
```

*** =type3:NormalExercise
*** =key3: 1496605dac
*** =xp3: 20

*** =instructions3
Finally, change 'SQL is' to 'SQL is cool!' and click Submit!

*** =hint3
Change the code and submit the query!

*** =solution3
```{sql}
SELECT 'SQL is cool!'
AS result;
```

*** =sct3
```{sql}
Ex().test_error()

Ex().test_student_typed('SQL is cool!', msg="Did you change the query correctly?", fixed=True)

Ex().test_has_columns()
Ex().check_result()
```

--- type:NormalExercise lang:sql xp:100 skills:1 key:7d7e325a12
## A note on errors

If you submit the code to the right, you'll see that you get two types of errors. _SQL_ errors are shown below the editor. You should see:

```
syntax error at or near "'DataCamp <3 SQL'" LINE 2: 'DataCamp <3 SQL' ^
```

_DataCamp_ errors are shown in the the **Instructions** box. These will let you know in plain English where you went wrong in your code! You should see:

```
You need to add SELECT at the start of line 2!
```

*** =instructions
Submit the code to the right, check out the errors, then fix them to start the course!

*** =hint
In the editor, change line 2 to `SELECT 'DataCamp <3 SQL'`.

*** =pre_exercise_code
```{python}
connect('postgresql', 'films')
```

*** =sample_code
```{sql}
-- Try running me!
'DataCamp <3 SQL'
AS result;
```

*** =solution
```{sql}
-- Try running me!
SELECT 'DataCamp <3 SQL'
AS result;
```

*** =sct
```{sql}
Ex().test_student_typed('SELECT', msg='You need to add `SELECT` at the start of line 2!', fixed=True)
Ex().test_has_columns()
Ex().test_error()
```

--- type:PlainMultipleChoiceExercise lang:sql xp:50 key:a1f556e63f
## Beginning your SQL journey

Now that you're familiar with the interface, let's get straight into it.

SQL, which stands for *Structured Query Language*, is a language for interacting with data stored in something called a *relational database*.

You can think of a relational database as a collection of tables. A table is just a set of rows and columns, like a spreadsheet, which represents exactly one type of entity. For example, a table might represent employees in a company or purchases made, but not both.

Each row, or *record*, of a table contains information about a single entity. For example, in a table representing employees, each row represents a single person. Each column, or *field*, of a table contains a single attribute for all rows in the table. For example, in a table representing employees, we might have a column containing first and last names for all employees.

The table of employees might look something like this:

| id | name | age | nationality |
|----|----|----|----|
| 1 | Jessica | 22 | Ireland
| 2 | Gabriel | 48 | France |
| 3 | Laura | 36 | USA |

<hr>
How many fields does the employees table above contain?

*** =instructions
- 1
- 2
- 3
- 4

*** =hint
Remember that in database lingo, a column is called a *field*. How many fields does the table contain?

*** =sct
```{python}
msg1 = "Incorrect, a table contains information about one type of entity, but generally has multiple fields."
msg2 = "Sorry, try again!"
msg3 = "Incorrect, the table contains three records, but how many fields does it have?"
success_msg = "Correct! The table contains four columns, or fields."

Ex().test_mc(4, [msg1, msg2, msg3, success_msg])
```

--- type:BulletExercise lang:sql xp:100 key:c0bb58f7f9
## SELECTing single columns

While SQL can be used to create and modify databases, the focus of this course will be *querying* databases. A *query* is a request for data from a database table (or combination of tables). Querying is an essential skill for a data scientist, since the data you need for your analyses will often live in databases.

In SQL, you can select data from a table using a `SELECT` statement. For example, the following query selects the `name` column from the `people` table:

```sql
SELECT name
FROM people;
```

In this query, `SELECT` and `FROM` are called keywords. In SQL, keywords are not case-sensitive, which means you can write the same query as:

```sql
select name
from people;
```

That said, it's good practice to make SQL keywords uppercase to distinguish them from other parts of your query, like column and table names.

It's also good practice (but not necessary for the exercises in this course) to include a semicolon at the end of your query. This tells SQL where the end of your query is!

*** =pre_exercise_code
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'people'])
```

*** =sample_code
```{sql}

```

*** =type1: NormalExercise
*** =key1: a41cc766d5
*** =xp1: 20
*** =instructions1
Select the `title` column from the `films` table. You can see your results in the query result tab to the right!
*** =solution1
```{sql}
SELECT title
FROM films;
```

*** =hint1
```
SELECT ___
FROM ___;
```
*** =sct1
```{python}
sel = check_node('SelectStmt')

title = test_column('title', msg='Did you select the `title` column correctly?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    title,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type2: NormalExercise
*** =key2: 4a74270ecd
*** =xp2: 20
*** =instructions2
Modify your query to get the `release_year` column from the `films table`.

*** =solution2
```{sql}
SELECT release_year
FROM films;
```
*** =hint2
```
SELECT ___
FROM ___;
```
*** =sct2
```{python}
sel = check_node('SelectStmt')

release_year = test_column('release_year', msg='Did you select the `release_year` column correctly?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    release_year,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type3: NormalExercise
*** =key3: 323bd5ddf5
*** =xp3: 20
*** =instructions3
Now modify your query to get the `name` of each person in the `people` table.

*** =solution3
```{sql}
SELECT name
FROM people;
```
*** =hint3
```
SELECT ___
FROM ___;
```
*** =sct3
```{python}
sel = check_node('SelectStmt')

name = test_column('name', msg='Did you select the `name` column correctly?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    name,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

--- type:BulletExercise lang:sql xp:100 key:09f21bae4c
## SELECTing multiple columns

Well done! Now you know how to select single columns.

In the real world, you will often want to select multiple columns. Luckily, SQL makes this really easy. To select multiple columns from a table, simply separate the column names with commas!

For example, this query selects two columns, `name` and `birthdate`, from the `people` table:

```sql
SELECT name, birthdate
FROM people;
```

Sometimes, you may want to select all columns from a table. Typing out every column name would be a pain, so there's a handy shortcut:

```sql
SELECT *
FROM people;
```

If you only want to return a certain number of results, you can use the `LIMIT` keyword to limit the number of rows returned:

```sql
SELECT *
FROM people
LIMIT 10;
```

Before getting started with the instructions below, check out the column names in the `films` table by clicking on the `films` tab to the right!

*** =pre_exercise_code
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

*** =sample_code
```{sql}
```

*** =type1: NormalExercise
*** =key1: d561b4df97
*** =xp1: 20
*** =instructions1
Get the title of every film from the `films` table.

*** =solution1
```{sql}
SELECT title
FROM films;
```

*** =hint1
```
SELECT ___
FROM ___;
```
*** =sct1
```{python}
sel = check_node('SelectStmt')

title = test_column('title', msg='Did you select the `title` column correctly?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` cause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    title,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type2: NormalExercise
*** =key2: 917d7dc533
*** =xp2: 20
*** =instructions2
Get the title and release year for every film.

*** =solution2
```{sql}
SELECT title, release_year
FROM films;
```
*** =hint2
```
SELECT ___, ___
FROM ___;
```
*** =sct2
```{python}
sel = check_node('SelectStmt')

title = test_column('title', msg='Did you select the `title` column correctly?')

release_year = test_column('release_year', msg='Did you select the `release_year` column correctly?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` cause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    title,
    release_year,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type3: NormalExercise
*** =key3: eeba078a00
*** =xp3: 20
*** =instructions3
Get the title, release year and country for every film.

*** =solution3
```{sql}
SELECT title, release_year, country
FROM films;
```

*** =hint3
```
SELECT ___, ___, ___
FROM ___;
```
*** =sct3
```{python}
sel = check_node('SelectStmt')

title = test_column('title', msg='Did you select the `title` column correctly?')

release_year = test_column('title', msg='Did you select the `release_year` column correctly?')

country = test_column('country', msg='Did you select the `country` column correctly?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` cause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    title,
    release_year,
    country,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type4: NormalExercise
*** =key4: dac27d9aad
*** =xp4: 20
*** =instructions4
Get all columns from the `films` table.
*** =solution4
```{sql}
SELECT *
FROM films;
```

*** =hint4
```
SELECT *
FROM ___;
```

*** =sct4
```{python}
sel = check_node('SelectStmt')

star = sel.check_node('Star').has_equal_ast('Did you use `SELECT *` to get all columns?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    star,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

--- type:BulletExercise lang:sql xp:100 key:de52236965
## SELECT DISTINCT

Often your results will include many duplicate values. If you want to select all the unique values from a column, you can use the `DISTINCT` keyword.

This might be useful if, for example, you're interested in knowing which languages are represented in the `films` table:

```sql
SELECT DISTINCT language
FROM films;
```

Remember, you can check out the data in the tables by clicking on the tabs to the right under the editor!

*** =pre_exercise_code
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'roles'])
```

*** =sample_code
```{sql}
```

*** =type1: NormalExercise
*** =key1: e6b81711f1
*** =xp1: 20
*** =instructions1
Get all the unique countries represented in the `films` table.

*** =solution1
```{sql}
SELECT DISTINCT country
FROM films;
```

*** =hint1
```
SELECT DISTINCT ___
FROM ___;
```
*** =sct1
```{python}
sel = check_node('SelectStmt')

distinct = sel.check_field('pref').has_equal_ast("Don't forget to use the `DISTINCT` keyword!")

country = test_column('country', msg='Did you select the `country` column?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    country,
    distinct,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type2: NormalExercise
*** =key2: 2cb9a4bf6a
*** =xp2: 20
*** =instructions2
Get all the different film certifications from the `films` table.
*** =solution2
```{sql}
SELECT DISTINCT certification
FROM films;
```

*** =hint2
```
SELECT DISTINCT ___
FROM ___;
```

*** =sct2
```{python}
sel = check_node('SelectStmt')

distinct = sel.check_field('pref').has_equal_ast("Don't forget to use the `DISTINCT` keyword!")

certification = test_column('certification', msg='Did you select the `certification` column?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    certification,
    distinct,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type3: NormalExercise
*** =key3: 26835d3029
*** =xp3: 20
*** =instructions3
Get the different types of film roles from the `roles` table.

*** =solution3
```{sql}
SELECT DISTINCT role
FROM roles;
```

*** =hint3
```
SELECT DISTINCT ___
FROM ___;
```
*** =sct3
```{python}
sel = check_node('SelectStmt')

distinct = sel.check_field('pref').has_equal_ast("Don't forget to use the `DISTINCT` keyword!")

role = test_column('role', msg='Did you select the `role` column?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    distinct,
    role,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

--- type:MultipleChoiceExercise lang:sql xp:50 key:97f97f5766
## Learning to COUNT

What if you want to count the number of employees in your employees table? The `COUNT` statement lets you do this by returning the number of rows in one or more columns.

For example, this code gives the number of rows in the `people` table:

```sql
SELECT COUNT(*)
FROM people;
```

<hr>
How many records are contained in the `reviews` table?

*** =instructions
- 9,468
- 8,397
- 4,968
- 9,837
- 9,864

*** =hint
Run a query to count the number of records in the `reviews` table!

*** =pre_exercise_code
```{python}
connect('postgresql', 'films')
```

*** =sample_code
```{sql}
-- You can test out queries here!

```

*** =sct
```{python}
success_msg = 'Correct!'
msg2 = "Use the syntax provided in the example. Be sure to swap out `people` for `reviews`!"

Ex().test_mc(3,[msg2, msg2, success_msg, msg2, msg2])
```
--- type:BulletExercise lang:sql xp:100 key:7643365e67
## Practice with COUNT

As you've seen, `COUNT(*)` tells you how many rows are in a table. However, if you want to count the number of *non-missing* values in a particular column, you can call `COUNT` on just that column.

For example, to count the number of birth dates present in the `people` table:

```sql
SELECT COUNT(birthdate)
FROM people;
```

It's also common to combine `COUNT` with `DISTINCT` to count the number of *distinct* values in a column.

For example, this query counts the number of distinct birth dates contained in the `people` table:

```sql
SELECT COUNT(DISTINCT birthdate)
FROM people;
```

Let's get some practice with `COUNT`!

*** =pre_exercise_code
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'people'])
```

*** =sample_code
```{sql}
```

*** =type1: NormalExercise
*** =key1: 4688067e3e
*** =xp1: 20
*** =instructions1
Count the number of rows in the `people` table.
*** =solution1
```{sql}
SELECT COUNT(*)
FROM people;
```

*** =hint1
```
SELECT COUNT(___)
FROM ___;
```
*** =sct1
```{python}
sel = check_node('SelectStmt')

temp = sel.check_node('Call')

count_call = temp.check_field('name').has_equal_ast('Are you calling the `COUNT` function?')

count_args = temp.check_field('args').has_equal_ast('Are you using `COUNT` on the right column?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    count_call,
    count_args,
    count_call,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type2: NormalExercise
*** =key2: 497ffa962e
*** =xp2: 20
*** =instructions2
Count the number of (non-missing) birth dates in the `people` table.
*** =solution2
```{sql}
SELECT COUNT(birthdate)
FROM people;
```
*** =hint2
```
SELECT ___(___)
FROM ___;
```
*** =sct2
```{python}
sel = check_node('SelectStmt')

temp = sel.check_node('Call')

count_call = temp.check_field('name').has_equal_ast('Are you calling the `COUNT` function?')

count_args = temp.check_field('args').has_equal_ast('Are you using `COUNT` on the right column?')

from_clause = count_call.has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    count_call,
    count_args,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type3: NormalExercise

*** =key3: 50c903a00a
*** =xp3: 20

*** =instructions3
Count the number of unique birth dates in the `people` table.
*** =solution3
```{sql}
SELECT COUNT(DISTINCT birthdate)
FROM people;
```
***=hint3
```
SELECT ___(DISTINCT ___)
FROM ___;
```
*** =sct3
```{python}
sel = check_node('SelectStmt')

temp = sel.check_node('Call')

count_call = temp.check_field('name').has_equal_ast('Are you using `COUNT` with `DISTINCT`?')

# not urgent: this might need to be changed
# count_distinct_arg = temp.check_field('pref').has_equal_ast('Are you using `DISTINCT` with `COUNT()`?')

count_args = temp.check_field('args').has_equal_ast('Are you using `COUNT` and `DISTINCT` with the right column?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    count_call,
    count_args,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type4: NormalExercise

*** =key4: 511052cbbe
*** =xp4: 20

*** =instructions4
Count the number of unique languages in the `films` table.
*** =solution4
```{sql}
SELECT COUNT(DISTINCT language)
FROM films;
```
*** =hint4
```
SELECT ___(DISTINCT ___)
FROM ___;
```
*** =sct4
```{python}
sel = check_node('SelectStmt')

temp = sel.check_node('Call')

count_call = temp.check_field('name').has_equal_ast('Are you using `COUNT` with `DISTINCT`?')

# not urgent: this might need to be changed
# count_distinct_arg = temp.check_field('pref').has_equal_ast('Are you using `DISTINCT` with `COUNT()`?')

count_args = temp.check_field('args').has_equal_ast('Are you using `COUNT` and `DISTINCT` with the right column?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    count_call,
    count_args,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```

*** =type5: NormalExercise

*** =key5: 9e1147efe5
*** =xp5: 20

*** =instructions5
Count the number of unique countries in the `films` table.
*** =solution5
```{sql}
SELECT COUNT(DISTINCT country)
FROM films;
```

*** =hint5
```
SELECT ___(DISTINCT ___)
FROM ___;
```

*** =sct5
```{python}
sel = check_node('SelectStmt')

temp = sel.check_node('Call')

count_call = temp.check_field('name').has_equal_ast('Are you using `COUNT` with `DISTINCT`?')

# not urgent: this might need to be changed
# count_distinct_arg = temp.check_field('pref').has_equal_ast('Are you using `DISTINCT` with `COUNT()`?')

count_args = temp.check_field('args').has_equal_ast('Are you using `COUNT` and `DISTINCT` with the right column?')

from_clause = sel.check_field('from_clause').has_equal_ast('Is your `FROM` clause correct?')

Ex().test_correct(check_result(), [
    from_clause,
    count_call,
    count_args,
    test_has_columns(),
    test_ncols(),
    test_error()
])
```
