# Introduction to MySQL
This practical work is about developing skills in SQL. Make sure you have had a look at the notes on key database concepts [Intro to Databases](intro-to-databases.md) and SQL [Intro to SQL](intro-to-sql.md) before attempting the following.

- [Follow these instructions if you are using Codespaces](#codespaces)
- [Follow these instruction if you are using XAMPP](#xampp)

## If you are using Codespaces <a name="codespaces"></a>
The codespace has a database installed. It also has a database management tool installed called Adminer.

- Select the 'ports' tab (next to terminal).
- Hover over the Forwarded port for 8081 and click 'Open in Browser'
- A new tab should open for Adminer.

To log into Adminer enter the following:-
- username: **root**
- password: **secret**
- database: **cht2520**

This will give you access to a database called **cht2520**.

Now move onto [Completing the practical work](#practical)

## If you are using XAMPP <a name="xampp"></a>
MySQL is part of XAMPP/MAMP/WAMP. To complete these exercises you will need Apache to be running and MySQL (check your control panel).

* In a web browser enter http://localhost/phpmyadmin/ and you will be taken to the login page for phpMyAdmin. It should also be available as a link from your localhost homepage.
* You may need to login as the administrator of MySQL.
    * On XAMPP/WAMP the username is *root* and the password is blank i.e. you don't enter anything.
    * On MAMP, I think the username is *root* and the password is *root*. Google it if it doesn't work.  

You should then be taken to the admin home screen with a list of databases down the left-hand side.

### Setting up a database
It's a good idea to set up a database where you can do all your work for the module. You will also need to set up a user with access to this database.

* From the navigation bar along the top select 'User accounts'.
* Select 'Add user account' and then enter the following details:
    * Username:cit2202
    * Host name: select 'Local'. It should fill the second field with 'localhost'.
    * Enter a password (and remember it!)
    * Scroll down a bit and select the checkbox that says *'Create database with same name and grant all privileges.'*
    * Scroll down to the bottom of the page and select 'Go'.

A database named cit2202 should appear on the left-hand side.
* Select this database. At the moment it will tell you 'No tables found'

## Completing the practical work <a name="practical"></a>
Select 'SQL Command' and enter the following SQL

```sql
CREATE TABLE films (
  id int(11) UNSIGNED NOT NULL AUTO_INCREMENT,
  title varchar(100) NOT NULL,
  year smallint(6) NOT NULL,
  duration smallint(6) NOT NULL,
  CONSTRAINT PRIMARY KEY (id)
)
```

Then click 'Execute'.
This SQL command creates a new table.
Next, we'll populate the table with some sample data. Enter the following SQL:

```sql
INSERT INTO `films` (`id`, `title`, `year`, `duration`) VALUES
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

- Hit 'Execute'
- Select the database and then select the films table and confirm you can see the films table.

### Inserting more data
Select the SQL navigation option.
-  Write your own INSERT statement to add another film to the table.

## Selecting data

* Select the SQL  navigation option, enter the following:-

```SQL
SELECT * FROM films WHERE title="Inception"
```
* Click 'go'. You should see the results of the query.

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
