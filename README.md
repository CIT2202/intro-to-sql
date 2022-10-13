# Introduction to MySQL
This practical work is about developing skills in SQL. Make sure you have had a look at the notes on key database concepts [Intro to Databases](intro-to-databases.md) and SQL [Intro to SQL](intro-to-sql.md) before attempting the following.

## If you are using XAMPP 
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

Now go onto *Creating some tables* below.

## If you are using selene
In a browser go to https://selene.hud.ac.uk/phpmyadmin/ . 
* The username and password are the same as the ones you have been using with FileZilla. 
* You will already have a database named after your student number set-up for you. It is on the left-hand side menu. Select this database. 

Now go on to creating some tables below.

## Creating some tables
Next, you need to import a table to use for this practical work.
* In phpMyAdmin from the navigation bar at the top select 'SQL'
* From GitHub select the file [films.sql](films.sql). This file contains some SQL commands that will create a database table and then insert some data into it.
    * Select the file, click *'raw'* and copy the entire contents of this file.
* Back in phpMyAdmin paste these SQL statements into the textbox labelled *'Run SQL query'*.
* Click 'Go'.
* Now if you select the database again you should see you have a *films* table
* Select this *films* table and it should allow you to browse the data in this table.

## Inserting more data
Select the SQL tab. This allows us to enter SQL commands and execute them.

* Paste in the following:
```SQL
INSERT INTO films (id, title, year, duration) VALUES (NULL, 'Parasite', 2019, 134)
```
* Click 'browse' you should be able to see a new row has been added to the database table
* Click on the SQL tab.
* Write your own INSERT statement to add another film to the table.

## Selecting data

* Select the SQL tab, enter the following

```SQL
SELECT * FROM films WHERE title="Inception"
```
* Click 'go'. You should see the results of the query.

* Write SELECT statements that will do the following (refer to the notes [Intro to SQL](intro-to-sql.md) to help you):
  * List all the films that were made in 2004
  * List all the films  with a duration of 100 minutes or greater
  * List these films in order, from the longest to the shortest
  * List all the films that have a title that contains the word 'the'
  * List all the films that have a title that starts with the word 'the'
  * List all the films that have a title that contains the word 'the' that weren't made in 2004
  * List all the films except for 'Mean Girls' and 'Get Out' that have a title that contains the letter 'g'
  * List the three shortest films
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
* Select the SQL tab
* Write an SQL statement to delete a film from the database table.
