# Introduction to MySQL
This practical work is about developing skills in SQL. Make sure you have had a look at the notes on key database concepts [Intro to Databases](intro-to-databases.md) and SQL [Intro to SQL](intro-to-sql.md) before attempting the following.

## Setting up the database

Open your existing codespace (DON'T CREATE A NEW ONE) [https://github.com/codespaces](https://github.com/codespaces).

Your codespace already has a database installed (MariaDB). It also has a database management tool installed called Adminer.

Select the 'ports' tab (next to terminal).
Hover over the forwarded port for 8080 and click 'Open in Browser'
A new tab should open for Adminer.

To log into Adminer enter the following:-
- username: **student**
- password: **secret**
- database: **webdev**

This will give you access to a database called **webdev**.

## Creating a Table

Select 'SQL Command' and enter attempt the following:

Write a `CREATE TABLE` statement for a `films` table. The table will need the following columns:-
- `id`. This will be the primary key and should be set to auto increment.
- `title`. This will store the title of a film e.g. 'Toy Story'
- `year`. This will store the year the film was released e.g. 1995
- `duration`. This will store the duration of the film in minutes e.g. 77

Add suitable constraints e.g. duration must be greater than 0. 

To test is this works try and run the following `INSERT` statement.

```sql
INSERT INTO films (id, title, year, duration) VALUES
(NULL, 'Toy Story', 1995, 77),
```
Check you can view this data in the table.
Write your own `INSERT` statement to add another film to the table.

Next, we'll populate the table with some additional sample data. Enter the following SQL:

```sql
INSERT INTO films (id, title, year, duration) VALUES
(NULL, 'Jaws', 1975, 124),
(NULL, 'Winter\'s Bone', 2010, 100),
(NULL, 'Do The Right Thing', 1989, 120),
(NULL, 'The Incredibles', 2004, 115),
(NULL, 'The Godfather', 1972, 177),
(NULL, 'Dangerous Minds', 1995, 99),
(NULL, 'Spirited Away', 2001, 124),
(NULL, 'Moonlight', 2016, 111),
(NULL, 'Life of PI', 2012, 127),
(NULL, 'Gravity', 2013, 91),
(NULL, 'Arrival', 2016, 116),
(NULL, 'Wonder Woman', 2017, 141),
(NULL, 'Mean Girls', 2004, 97),
(NULL, 'Inception', 2010, 108),
(NULL, 'Donnie Darko', 2001, 113),
(NULL, 'Get Out', 2017, 117);
```

- Check this has worked by selecting the films tables and then 'view data'.


## Selecting data

```SQL
SELECT * FROM films WHERE title="Inception"
```
* Click 'Go/Execute'. You should see the results of the query.

* Write SELECT statements that will do the following (refer to the notes [Intro to SQL](intro-to-sql.md) to help you):
  * List all the films that were made in 2004
  * List all the films  with a duration of 100 minutes or greater
  * List these films in order, from the longest duration to the shortest
  * List all the films that have a title that contains the word 'the'
  * List all the films that have a title that starts with the word 'the'
  * List all the films that have a title that contains the word 'the' that weren't made in 2004
  * List all the films except for 'Mean Girls' and 'Get Out' that have a title that contains the letter 'g'
  * List the three shortest (in terms of duration) films
  * List the 4th and 5th oldest films
  * List the total duration of all the films in the table
  * List all the different years (no duplicates) in the table
  * Display the number of films in the table
  * Display the average duration of all the films in the database
  * Display the average duration of all the films made in the 21st century
  * List each year and the number of films made in that year
  * List each year. For each year, display the average duration of all the films made in that year, order the results in ascending order
  * Modify the above by rounding the duration of each film to the nearest minute (you might have to do some extra research)
    

## Deleting data
* Write an SQL statement to delete a film from the database table.
* Confirm this works.
