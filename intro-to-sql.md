# Intro to SQL

To work with a database we issue commands to the RDBMS using a language called Structured Query Language (SQL).

We can issues these commands in a number of different ways e.g.
* From within our PHP code.
* Using a command line interface.
* Using a web interface (e.g. phpmyadmin/adminer)

There are SQL commands for creating databases and tables. We are going to skip these. This module isn't about designing or creating databases. It is about working with a database using PHP so we are interested in the basic CRUD operations (Create, Read, Update, Delete) on a table.

Consider the following table:

**students**

| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
|   |    |        |               |    |
|   |   |         |               |    |
|   |     |        |        |    |
|   |     |       |   |    |
|   |      |       |        |    |


## Inserting Data
Running the following SQL statement

```sql
INSERT INTO students (id, last_name, first_name, course, mark)
VALUES (NULL , 'Compton', 'Jane', 'IT', 58);
```

Would result in:

| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 1  | Compton   | Jane       | IT              | 58   |

Note **NULL** was entered for the id value. This is because the table was set up to use a surrogate key with an AUTO_INCREMENT id column. MySQL will automatically generate the next available unique id number if we enter NULL for the id value.

We can insert multiple rows e.g.

```sql
INSERT INTO students
(id, last_name, first_name, course, mark)
VALUES
(NULL, 'Atherton', 'Ian', 'IT', 32),
(NULL, 'Hutton', 'Kate', 'Web Design', 72),
(NULL, 'Laxman', 'Sunil', 'Web Programming', 52),
(NULL, 'Crowe', 'Grace', 'Computing', 70);
```
**students**

| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 1  | Compton   | Jane       | IT              | 58   |
| 2  | Atherton  | Ian        | IT              | 32   |
| 3  | Hutton    | Kate       | Web Design      | 72   |
| 4  | Laxman    | Sunil      | Web Programming | 52   |
| 5  | Crowe     | Grace      | Computing       | 70   |

## The SELECT statement
The most commonly used SQL statement is SELECT. It is used to retrieve data from the database.

Imagine a search facility on a website. The user enters a search term and we would then execute a SELECT statement to find all the records that match the search criteria.

### Selecting specific columns
We can specify which columns we want to retrieve e.g.
```sql
SELECT last_name, first_name FROM students;
```
| last_name | first_name |
|-----------|------------|
| Compton   | Jane       |
| Atherton  | Ian        |
| Hutton    | Kate       |
| Laxman    | Sunil      |
| Crowe     | Grace      |

We specify all the columns with an asterix (*)

```sql
SELECT * FROM students;
```
| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 1  | Compton   | Jane       | IT              | 58   |
| 2  | Atherton  | Ian        | IT              | 32   |
| 3  | Hutton    | Kate       | Web Design      | 72   |
| 4  | Laxman    | Sunil      | Web Programming | 52   |
| 5 | Crowe     | Grace      | Computing       | 70   |

### DISTINCT
We can use the DISTINCT key word to remove duplicates from the results
```sql
SELECT DISTINCT course FROM students;
```
| course          |
|-----------------|
| IT              |
| Web Design      |
| Web Programming |
| Computing       |

Note that IT only appears once in the results.

### WHERE
We can choose to retrieve specific rows using a WHERE clause e.g. If I want to know the names of all the students on the IT course.
```sql
SELECT * FROM students WHERE course = "IT";
```
| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 1  | Compton   | Jane       | IT              | 58   |
| 2  | Atherton  | Ian        | IT              | 32   |

There are other conditional operators we can use
* ```=``` Equal to
* ```<``` Less than
* ```>``` Greater than
* ```<=``` Less than or equal to
* ```>=``` Greater than or equal to
* ```<>``` Not equal to

Here's an example that uses the ```>=``` operator.
```sql
SELECT last_name, firstname
FROM students
WHERE mark >= 40
```

| last_name | first_name |
|-----------|------------|
| Compton   | Jane       |
| Hutton    | Kate       |
| Laxman    | Sunil      |
| Crowe     | Grace      |

#### The LIKE Operator
The LIKE operator works with strings and allows for 'fuzzy matching'. The % sign is used as a wildcard.

```sql
SELECT * FROM students WHERE last_name LIKE '%xyz';
```
Would match all strings that end in 'xyz'
 e.g. 'wxyz' or 'some text xyz'.
```sql
SELECT * FROM students WHERE last_name LIKE 'abc%';
```
Would match all strings that start with 'abc'
e.g.'abcd' or 'abc some text'.
```sql
 SELECT * FROM students WHERE last_name LIKE '%abc%';
 ```
Would match all strings that start contain the string 'abc' e.g.'abcd',
'abc some text' or 'something abc' or 'something abc else'.

Imagine we want to know the last name and mark of all the students studying Web Design or Web Programming
The LIKE clause allows us to select any students with the text 'Web' somewhere in the course title.

```sql
SELECT * FROM students WHERE course LIKE '%Web%';
```

| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 3  | Hutton    | Kate       | Web Design      | 72   |
| 4 | Laxman    | Sunil      | Web Programming | 52   |

#### IN and NOT IN
We can test columns against a set of values using IN e.g. if I want details of all the students on IT or Computing.
```sql
SELECT * FROM students WHERE course IN ("IT", "Computing");
```
| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 1  | Compton   | Jane       | IT              | 58   |
| 2  | Atherton  | Ian        | IT              | 32   |
| 5  | Crowe     | Grace      | Computing       | 70   |

There is also a NOT IN which can be used to exclude rows from the results.

#### AND and OR
We can use the AND and OR operators to perform two or more tests in a single statement e.g. if we wanted to know the details of all the IT students with a mark over 50.

```sql
SELECT last_name, first_name FROM students WHERE course = "IT" AND mark >50;
```
| last_name | first_name |
|-----------|------------|
| Compton   | Jane       |

### ORDER BY
The ORDER BY clause is used to sort the output and present it in either ascending (ASC) or descending (DESC) order. The default is ascending order. We can order numeric or string data.

```sql
SELECT * FROM students ORDER BY mark DESC
```
| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 3  | Hutton    | Kate       | Web Design      | 72   |
| 5  | Crowe     | Grace      | Computing       | 70   |
| 1  | Compton   | Jane       | IT              | 58   |
| 4  | Laxman    | Sunil      | Web Programming | 52   |
| 2  | Atherton  | Ian        | IT              | 32   |

### LIMIT and OFFSET
We can limit the number of results returned e.g.
```sql
SELECT * FROM students ORDER BY mark DESC LIMIT 3
```
| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 3  | Hutton    | Kate       | Web Design      | 72   |
| 5 | Crowe     | Grace      | Computing       | 70   |
| 1  | Compton   | Jane       | IT              | 58   |

We can use OFFSET to skip results from the start of the results e.g.

```sql
SELECT * FROM students ORDER BY mark DESC LIMIT 2 OFFSET 2
```
| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 1  | Compton   | Jane       | IT              | 58   |
| 4  | Laxman    | Sunil      | Web Programming | 52   |

### COUNT
The COUNT function tells us how many rows have been found. The AS is used to specify a name for the new column.
```sql
SELECT COUNT(*) AS 'Number of students' FROM  students
```
| Number of students |
|----|
| 5 |

### GROUP BY
We can group rows together and count the size of the groups.

```sql
SELECT course, COUNT(course) as "No. students"
FROM  students
GROUP BY course
```
| course          | No. Students |
|-----------------|------|
| Web Design      | 1   |
| Computing       | 1   |
| IT              | 2   |
| Web Programming | 1   |

### Aggregate functions
The AVG() function works out an average e.g.

```sql
SELECT AVG (mark) AS Average FROM students;
```
| Average         |
|-----------------|
| 56.8      |

We can also work out minimum and maximum values for groups using the MIN() and MAX() functions and add all the values of a group of rows using the SUM() function.

### Combining different operators and clauses
Many of these operators and clauses can be used in combination with each other e.g.

```sql
SELECT * FROM students WHERE mark > 50
AND course NOT IN("IT", "Computing")
ORDER BY last_name ASC
LIMIT 1
```
| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 4  | Laxman    | Sunil      | Web Programming | 52   |

## Updating Records
Using the UPDATE statement we can change the value of the a field e.g.
```sql
UPDATE students SET course= 'IT' WHERE id = 4
```
| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 1  | Compton   | Jane       | IT              | 58   |
| 2  | Atherton  | Ian        | IT              | 32   |
| 3  | Hutton    | Kate       | Web Design      | 72   |
| 4  | Laxman    | Sunil      | IT | 52   |
| 5  | Crowe     | Grace      | Computing       | 70   |

## Deleting Records
We can also delete rows e.g.
```sql
DELETE FROM students WHERE id = 4
```
| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 1  | Compton   | Jane       | IT              | 58   |
| 2  | Atherton  | Ian        | IT              | 32   |
| 3  | Hutton    | Kate       | Web Design      | 72   |
| 5  | Crowe     | Grace      | Computing       | 70   |
