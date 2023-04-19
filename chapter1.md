---
title: Selecting columns
description: >-
  This chapter provides a brief introduction to working with relational
  databases. You'll learn about their structure, how to talk about them using
  database lingo, and how to begin an analysis using simple SQL commands to
  select and summarize columns from database tables.
free_preview: true
attachments:
  slides_link: >-
    https://s3.amazonaws.com/assets.datacamp.com/production/course_1946/slides/chapter1.pdf
lessons:
  - nb_of_exercises: 5
    title: Welcome to the course!
  - nb_of_exercises: 4
    title: SELECTing columns
  - nb_of_exercises: 2
    title: Learning to COUNT
---

## Welcome to the course!

```yaml
type: VideoExercise
key: dcdbb24914
lang: sql
xp: 50
skills:
  - 1
```

`@projector_key`
f05d06ad7807cf476fdb5f674174c9d5

---

## Onboarding | Tables

```yaml
type: MultipleChoiceExercise
key: e456699517
lang: sql
xp: 50
skills:
  - 1
```

The DataCamp interface for SQL courses contains a few unique features you should be aware of.

For this course, you'll be using a database containing information on almost 5000 films. At the top of the screen, above the exercise text, you can see the data in this database by tapping on the table names. 

From looking at the table, who is the first person listed in the `people` table?

`@possible_answers`
- Kanye West
- Biggie Smalls
- 50 Cent
- Jay Z

`@hint`
Look at the `people` table at the top of the exercise!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
```

`@sct`
```{python}
patt = '%s is nowhere to be seen in the `people` table. Have another look!'
msg1 = patt % "Kanye West"
msg2 = patt % "Biggie Smalls"
msg3 = "That's correct! Head over to the next exercise to see how we can answer a similar question with code!"
msg4 = patt % "Jay Z"
Ex().has_chosen(3,[msg1, msg2, msg3, msg4])
```

---

## Onboarding | Query Result

```yaml
type: MultipleChoiceExercise
key: 5314676aac
lang: sql
xp: 50
skills:
  - 1
```

Notice the **Query** and the **Result** tabs at the top of your screen. The **Query** tab contains the query editor that you will use to write the code. The results of your SQL queries will be displayed in the **Result** tab.

Type this query in the editor in the **Query** tab, then tap **Run Code**, and check out the resulting table in the **Result** tab!

```{sql}
SELECT name FROM people;
```

Who is the second person listed in the query result?

`@possible_answers`
- Kanye West
- A. Michael Baldwin
- 50 Cent
- Jay Z

`@hint`
Run the code in the editor and look at the result tab at the top of the screen!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
```

`@sct`
```{python}
patt = "If you execute the query that was already provided with the 'Run Code' button, you will see that %s is not the second person listed in the query result."
msg1 = patt % "Kanye West"
msg2 = "Correct!"
msg3 = "50 Cent is the first person listed in the query result. We're looking for the second person."
msg4 = patt % "Jay Z"
Ex().has_chosen(2, [msg1, msg2, msg3, msg4])
```

---

## Onboarding | Errors

```yaml
type: NormalExercise
key: 7d7e325a12
lang: sql
xp: 100
skills:
  - 1
```

If you submit the code that's written in the **Query** tab, you'll see that you get two types of errors.


_SQL_ errors are shown in the **Result** tab. These are errors returned by the _SQL engine_. You should see:

```
syntax error at or near "'DataCamp <3 SQL'" LINE 2: 'DataCamp <3 SQL' ^
```
<br>
_DataCamp_ errors are shown in the **Incorrect submission** box. These will let you know in plain English where you went wrong in your code! You should see:

```
Alright, now go ahead and fix your code by including a `SELECT`.
```

`@instructions`
Submit the code below, check out the errors, then fix them!

`@hint`
In the editor, change line 2 to `SELECT 'DataCamp <3 SQL'`.

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
```

`@sample_code`
```{sql}
-- Try running me!
'DataCamp <3 SQL'
AS result;
```

`@solution`
```{sql}
-- Try running me!
SELECT 'DataCamp <3 SQL'
AS result;
```

`@sct`
```{sql}
Ex().has_code(r'SELECT|select|Select', incorrect_msg="Alright, now go ahead and fix your code by including a `SELECT` before `'DataCamp <3 SQL'`.")

Ex().check_column('result').has_equal_value()

Ex().success_msg("Excellent error editing! You can feel safe experimenting with code in the editor &ndash; you'll always get feedback if something goes wrong.")
```

---

## Onboarding | Multi-step Exercises

```yaml
type: BulletExercise
key: 81eb00a53d
lang: sql
xp: 100
skills:
  - 1
```

The following multi-step exercise allows you to practice a new concept through repetition. Check it out!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
```

***

```yaml
type: NormalExercise
key: 157ee8d1ad
xp: 35
```

`@instructions`
Submit the query in the editor! Don't worry, you'll learn how it works soon.

`@hint`
Submit the query!

`@sample_code`
```{sql}
SELECT 'SQL'
AS result;
```

`@solution`
```{sql}
SELECT 'SQL'
AS result;
```

`@sct`
```{sql}
Ex().check_column('result').has_equal_value()
```

***

```yaml
type: NormalExercise
key: 764f82129d
xp: 35
```

`@instructions`
Now change `'SQL'` to `'SQL is'` and click Submit!

`@hint`
Change the code and submit the query!

`@sample_code`
```{sql}
SELECT 'SQL'
AS result;
```

`@solution`
```{sql}
SELECT 'SQL is'
AS result;
```

`@sct`
```{sql}
Ex().check_correct(
    check_column('result').has_equal_value(),
    has_code('SQL is', incorrect_msg="Did you change `'SQL'` to `'SQL is'`?.", fixed=True)
)
```

***

```yaml
type: NormalExercise
key: 1496605dac
xp: 30
```

`@instructions`
Finally, change `'SQL is'` to `'SQL is cool'` and click Submit!

`@hint`
Change the code and submit the query!

`@sample_code`
```{sql}
SELECT 'SQL is'
AS result;
```

`@solution`
```{sql}
SELECT 'SQL is cool'
AS result;
```

`@sct`
```{sql}
Ex().check_correct(
    check_column('result').has_equal_value(),
    has_code('SQL is cool', incorrect_msg="Did you change `'SQL is'` to `'SQL is cool'`?", fixed=True)
)
Ex().success_msg("Well done! The time has come to actually fetch information from tables now!")
```

---

## Beginning your SQL journey

```yaml
type: PureMultipleChoiceExercise
key: a1f556e63f
lang: sql
xp: 50
```

Now that you're familiar with the interface, let's get straight into it.

SQL, which stands for *Structured Query Language*, is a language for interacting with data stored in something called a *relational database*.

You can think of a relational database as a collection of tables. A table is just a set of rows and columns, like a spreadsheet, which represents exactly one type of entity. For example, a table might represent employees in a company or purchases made, but not both.

Each row, or *record*, of a table contains information about a single entity. For example, in a table representing employees, each row represents a single person. Each column, or *field*, of a table contains a single attribute for all rows in the table. For example, in a table representing employees, we might have a column containing first and last names for all employees.

The table of employees might look something like this:

```out
| id | name    | age | nationality |
|----|---------|-----|-------------|
| 1  | Jessica | 22  | Ireland     |
| 2  | Gabriel | 48  | France      |
| 3  | Laura   | 36  | USA         |

```
<hr>

How many fields does the employees table above contain?

`@hint`
Remember that in database lingo, a column is called a *field*. How many fields does the table contain?

`@possible_answers`
- 1
- 2
- 3
- [4]

`@feedback`
- Incorrect, a table contains information about one type of entity, but generally has multiple fields.
- Sorry, try again!
- Incorrect, the table contains three records, but how many fields does it have?
- Correct! The table contains four columns, or fields.

---

## SELECTing single columns

```yaml
type: BulletExercise
key: c0bb58f7f9
lang: sql
xp: 100
```

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

Remember, you can see the results of executing your query in the __query__ tab!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'people'])
```

***

```yaml
type: NormalExercise
key: a41cc766d5
xp: 35
```

`@instructions`
Select the `title` column from the `films` table.

`@hint`
```
SELECT ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT title
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('title').has_equal_value(),
    check_node('SelectStmt').multi(
        check_edge('target_list', 0).has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )   
)
```

***

```yaml
type: NormalExercise
key: 4a74270ecd
xp: 35
```

`@instructions`
Select the `release_year` column from the `films` table.

`@hint`
```
SELECT ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT release_year
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('release_year').has_equal_value(),
    check_node('SelectStmt').multi(
        check_edge('target_list', 0).has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )   
)
```

***

```yaml
type: NormalExercise
key: 323bd5ddf5
xp: 30
```

`@instructions`
Select the `name` of each person in the `people` table.

`@hint`
```
SELECT ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT name
FROM people;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('name').has_equal_value(),
    check_node('SelectStmt').multi(
        check_edge('target_list', 0).has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )   
)
```

---

## SELECTing multiple columns

```yaml
type: BulletExercise
key: 09f21bae4c
lang: sql
xp: 100
```

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

Before getting started with the instructions below, check out the column names in the `films` table!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films'])
```

***

```yaml
type: NormalExercise
key: d561b4df97
xp: 25
```

`@instructions`
Get the title of every film from the `films` table.

`@hint`
```
SELECT ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT title
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('title').has_equal_value(),
    check_node('SelectStmt').multi(
        check_edge('target_list', 0).has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )   
)
```

***

```yaml
type: NormalExercise
key: 917d7dc533
xp: 25
```

`@instructions`
Get the title and release year for every film.

`@hint`
```
SELECT ___, ___
FROM ___;
```

`@sample_code`
```{sql}
SELECT title
FROM films;
```

`@solution`
```{sql}
SELECT title, release_year
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    multi(
        check_column('title').has_equal_value(),
        check_column('release_year').has_equal_value()
    ),
    check_node('SelectStmt').multi(
        check_edge('target_list', 0).has_equal_ast(),
        check_edge('target_list', 1).has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )   
)
```

***

```yaml
type: NormalExercise
key: eeba078a00
xp: 25
```

`@instructions`
Get the title, release year and country for every film.

`@hint`
```
SELECT ___, ___, ___
FROM ___;
```

`@sample_code`
```{sql}
SELECT title, release_year
FROM films;
```

`@solution`
```{sql}
SELECT title, release_year, country
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    multi(
        check_column('title').has_equal_value(),
        check_column('release_year').has_equal_value(),
        check_column('country').has_equal_value()
    ),
    check_node('SelectStmt').multi(
        check_edge('target_list', 0).has_equal_ast(),
        check_edge('target_list', 1).has_equal_ast(),
        check_edge('target_list', 2).has_equal_ast(),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: dac27d9aad
xp: 25
```

`@instructions`
Get all columns from the `films` table.

`@hint`
```
SELECT *
FROM ___;
```

`@sample_code`
```{sql}
SELECT title, release_year, country
FROM films;
```

`@solution`
```{sql}
SELECT *
FROM films;
```

`@sct`
```{python}
Ex().check_correct(
    check_all_columns().has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Star', missing_msg="Are you using `SELECT *` to select _all_ columns?"),
        check_edge('from_clause').has_equal_ast()
    )
)
```

---

## SELECT DISTINCT

```yaml
type: BulletExercise
key: de52236965
lang: sql
xp: 100
```

Often your results will include many duplicate values. If you want to select all the unique values from a column, you can use the `DISTINCT` keyword.

This might be useful if, for example, you're interested in knowing which languages are represented in the `films` table:

```sql
SELECT DISTINCT language
FROM films;
```

Remember, you can check out the data in the tables by clicking on the table name!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'roles'])
```

***

```yaml
type: NormalExercise
key: e6b81711f1
xp: 35
```

`@instructions`
Get all the unique countries represented in the `films` table.

`@hint`
```
SELECT DISTINCT ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT DISTINCT country
FROM films;
```

`@sct`
```{python}
distinct_msg = "Did you use the `DISTINCT` keyword?"
country_msg = "Did you use `DISTINCT country` to `SELECT` unique countries?"
Ex().check_correct(
    check_column('country').has_equal_value(),
    check_node('SelectStmt').multi(
        check_edge('pref', missing_msg=distinct_msg).has_equal_ast(incorrect_msg=distinct_msg),
        check_edge('target_list', 0).has_equal_ast(incorrect_msg=country_msg),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 2cb9a4bf6a
xp: 35
```

`@instructions`
Get all the different film certifications from the `films` table.

`@hint`
```
SELECT DISTINCT ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT DISTINCT certification
FROM films;
```

`@sct`
```{python}
distinct_msg = "Did you use the `DISTINCT` keyword?"
certs_msg = "Did you use `DISTINCT certification` to `SELECT` unique certifications?"
Ex().check_correct(
    check_column('certification').has_equal_value(),
    check_node('SelectStmt').multi(
        check_edge('pref', missing_msg=distinct_msg).has_equal_ast(incorrect_msg=distinct_msg),
        check_edge('target_list', 0).has_equal_ast(incorrect_msg=certs_msg),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 26835d3029
xp: 30
```

`@instructions`
Get the different types of film roles from the `roles` table.

`@hint`
```
SELECT DISTINCT ___
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT DISTINCT role
FROM roles;
```

`@sct`
```{python}
distinct_msg = "Did you use the `DISTINCT` keyword?"
role_msg = "Did you use `DISTINCT role` to `SELECT` unique roles?"
Ex().check_correct(
    check_column('role').has_equal_value(),
    check_node('SelectStmt').multi(
        check_edge('pref', missing_msg=distinct_msg).has_equal_ast(incorrect_msg=distinct_msg),
        check_edge('target_list', 0).has_equal_ast(incorrect_msg=role_msg),
        check_edge('from_clause').has_equal_ast()
    )
)
```

---

## Learning to COUNT

```yaml
type: MultipleChoiceExercise
key: 97f97f5766
lang: sql
xp: 50
```

What if you want to count the number of employees in your employees table? The `COUNT()` function lets you do this by returning the number of rows in one or more columns.

For example, this code gives the number of rows in the `people` table:

```sql
SELECT COUNT(*)
FROM people;
```

<hr>
How many records are contained in the `reviews` table?

`@possible_answers`
- 9,468
- 8,397
- 4,968
- 9,837
- 9,864

`@hint`
Run a query to count the number of records in the `reviews` table!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
```

`@sct`
```{python}
crm = 'Correct!'
icm = "Use the syntax provided in the example. Be sure to swap out `people` for `reviews`!"
Ex().has_chosen(3, [icm, icm, crm, icm, icm])
```

---

## Practice with COUNT

```yaml
type: BulletExercise
key: 7643365e67
lang: sql
xp: 100
```

As you've seen, `COUNT(*)` tells you how many rows are in a table. However, if you want to count the number of *non-missing* values in a particular column, you can call `COUNT()` on just that column.

For example, to count the number of birth dates present in the `people` table:

```sql
SELECT COUNT(birthdate)
FROM people;
```

It's also common to combine `COUNT()` with `DISTINCT` to count the number of *distinct* values in a column.

For example, this query counts the number of distinct birth dates contained in the `people` table:

```sql
SELECT COUNT(DISTINCT birthdate)
FROM people;
```

Let's get some practice with `COUNT()`!

`@pre_exercise_code`
```{python}
connect('postgresql', 'films')
set_options(visible_tables = ['films', 'people'])
```

***

```yaml
type: NormalExercise
key: 4688067e3e
xp: 20
```

`@instructions`
Count the number of rows in the `people` table.

`@hint`
```
SELECT COUNT(___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT COUNT(*)
FROM people;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('count').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call').multi(
            check_edge('name').has_equal_ast(incorrect_msg="Are you calling the `COUNT()` function?"),
            check_edge('args').has_equal_ast(incorrect_msg='Are you using `COUNT(*)`?')
        ),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 497ffa962e
xp: 20
```

`@instructions`
Count the number of (non-missing) birth dates in the `people` table.

`@hint`
```
SELECT ___(___)
FROM ___;
```

`@sample_code`
```{sql}
SELECT COUNT(*)
FROM people;
```

`@solution`
```{sql}
SELECT COUNT(birthdate)
FROM people;
```

`@sct`
```{python}
Ex().check_correct(
    check_column('count').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call').multi(
            check_edge('name').has_equal_ast(incorrect_msg="Are you calling the `COUNT()` function?"),
            check_edge('args').has_equal_ast(incorrect_msg='Are you using `COUNT(birthdate)`?')
        ),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 50c903a00a
xp: 20
```

`@instructions`
Count the number of unique birth dates in the `people` table.

`@hint`
```
SELECT ___(DISTINCT ___)
FROM ___;
```

`@sample_code`
```{sql}
SELECT COUNT(birthdate)
FROM people;
```

`@solution`
```{sql}
SELECT COUNT(DISTINCT birthdate)
FROM people;
```

`@sct`
```{python}
hint = "Are you using `COUNT(DISTINCT birthdate)`?"
Ex().check_correct(
    check_column('count').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call').multi(
            check_edge('name').has_equal_ast(incorrect_msg="Are you calling the `COUNT()` function?"),
            check_edge('pref').has_equal_ast(incorrect_msg=hint),
            check_edge('args').has_equal_ast(incorrect_msg=hint)
        ),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 511052cbbe
xp: 20
```

`@instructions`
Count the number of unique languages in the `films` table.

`@hint`
```
SELECT ___(DISTINCT ___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT COUNT(DISTINCT language)
FROM films;
```

`@sct`
```{python}
hint = "Are you using `COUNT(DISTINCT language)`?"
Ex().check_correct(
    check_column('count').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call').multi(
            check_edge('name').has_equal_ast(incorrect_msg="Are you calling the `COUNT()` function?"),
            check_edge('pref').has_equal_ast(incorrect_msg=hint),
            check_edge('args').has_equal_ast(incorrect_msg=hint)
        ),
        check_edge('from_clause').has_equal_ast()
    )
)
```

***

```yaml
type: NormalExercise
key: 9e1147efe5
xp: 20
```

`@instructions`
Count the number of unique countries in the `films` table.

`@hint`
```
SELECT ___(DISTINCT ___)
FROM ___;
```

`@sample_code`
```{sql}

```

`@solution`
```{sql}
SELECT COUNT(DISTINCT country)
FROM films;
```

`@sct`
```{python}
hint = "Are you using `COUNT(DISTINCT country)`?"
Ex().check_correct(
    check_column('count').has_equal_value(),
    check_node('SelectStmt').multi(
        check_node('Call').multi(
            check_edge('name').has_equal_ast(incorrect_msg="Are you calling the `COUNT()` function?"),
            check_edge('pref').has_equal_ast(incorrect_msg=hint),
            check_edge('args').has_equal_ast(incorrect_msg=hint)
        ),
        check_edge('from_clause').has_equal_ast()
    )
)
```
