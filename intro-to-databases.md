# Intro to Databases
Most useful websites store information in some way. To store or save data we use a database.
A database is simply a collection of data that is stored in a structured way. There a lots of different types of database e.g. NoSQL, Relational, Graph. We will be working with relational databases in this module.

## DBMS (Database Management System)
* A database Management System is simply software that manages the data in a database. We issue commands to a DBMS to perform actions such as creating new databases, adding data to a database, retrieving data from a database and deleting data from a database
* The DBMS we will be using is **MySQL** (sometimes we use a version called **MariaDB** but it is essentially the same thing). There are other relation DBMS which are commonly used with PHP e.g. PostgreSQL.

## Key Relational Database Concepts
* Relational databases are made up of one or more tables. Here's an example of a table:

  **students**

  | last_name | first_name | course          | mark |
  |-----------|------------|-----------------|------|
  | Compton   | Jane       | IT              | 58   |
  | Atherton  | Ian        | IT              | 32   |
  | Hutton    | Kate       | Web Design      | 72   |
  | Miandad   | Yousef     | IT              | 61   |
  | Laxman    | Sunil      | Web Programming | 52   |
  | Crowe     | Grace      | Computing       | 70   |
  | Hutton    | Marcus     | Web Design      | 42   |

* Each table stores information about a specific 'thing' or entity, in this example **students**.
* Tables are made up of a number **columns**, sometimes these are called **attributes**. In the above example *last_name*, *first_name*, *course* and *mark* are all columns
* Each **row** or **record** in the table stores information for a specific item, in this example a specific student.
* A specific cell in a table is called a **field** e.g. the *last_name* field for the first row in the table has a value of *Compton*. A **field** should only ever contain a single value. This can be text, a number, a date etc. but never multiple values.

> This table, like most of the tables in these notes, has several design flaws e.g. lots of duplication. This is mainly because we are only considering simple databases made up of a single table. Later on we will look at databases that feature multiple tables that can address these design flaws. 

## Primary Keys
There are key actions that we want to perform on a database table, often these are described using the acronym CRUD.
* C - Create, insert a new row into a table.
* R - Read, retrieve data from a table.
* U - Update, modify or change the data in a row.
* D - Delete, remove a row from a database table.

Imagine we want to delete the second row in the above table. We could give a command such as *'Delete the row where the last_name field equals Atherton'*.

But what if we wanted to delete the third row. We couldn't use the command *'Delete the row where the last_name field equals Hutton'* because there are two rows where the **last_name** is 'Hutton'. The DBMS wouldn't know which to delete.

What we need is a way of uniquely identifying a row in a table and this is what a primary key is.

> A primary key is a column or group of columns that uniquely identify a row

In the above table we could use the combination of **last_name** and **first_name** as our primary key e.g. *'Delete the row where the last_name field equals Hutton **and** the first_name field equals Kate'*

If we use two or more columns we call this a **composite** (or sometimes a **compound**) primary key.

> You might think we could just state *delete the third row*, but often we don't know how many rows there are in a table and if we delete a row all the subsequent rows will be re-numbered and there isn't an easy way we can keep track of this.

This composite primary key would work okay for the above table, but if we add more rows eventually we are going to end up with two students with the same first and last names.  

So what we can do is add another column to the table. This isn't based on any data from the real word it exists simply to make an easy to use primary key. We call this a **surrogate** key e.g. we could add an **id** column.

| id | last_name | first_name | course          | mark |
|----|-----------|------------|-----------------|------|
| 1  | Compton   | Jane       | IT              | 58   |
| 2  | Atherton  | Ian        | IT              | 32   |
| 3  | Hutton    | Kate       | Web Design      | 72   |
| 5  | Laxman    | Sunil      | Web Programming | 52   |
| 6  | Crowe     | Grace      | Computing       | 70   |
| 7  | Hutton    | Marcus     | Web Design      | 42   |

When we create a database table we can tell the DBMS to automatically generate this *id* value for us whenever a new row is added. We call this **auto_increment**.

On more bit of terminology you will come across
*  **candidate** key. This is the minimum group of columns that could be the primary key. So in the above example *id* is the candidate key.
* **natural** key. If we use a key formed by columns used in the real word we say it is a **natural** key e.g. if we had used a composite key of *last_name* and *first_name*.

Here are a couple more examples of tables and primary keys.

**airports**

| airport_code | name                    | city      |
|--------------|-------------------------|-----------|
| LHR          | London Heathrow Airport | London    |
| YBB          | Kugaaruk Airport        | Pelly Bay |
| PKR          | Pokhara Airport         | Pokhura   |
| ZMB          | Hamburg Hbf             | Hamburg   |

This table stores information about different airports. Each airport has a unique three letter code e.g. LHR. So in this table the **airport_code** would be a good choice for the primary key.

**footballers**

| name | team              | goals |
|------------|-------------------|-------|
| Rooney    | Manchester United | 183   |
| Gerard       | Liverpool         | 120    |
| Rooney    | Everton       | 25  |
| Agüero     | Manchester City | 184   |
| Scholes     | Manchester United | 107   |

This table stores footballers and how many goals they have scored for a particular team. We can't use *name* as the primary key (Rooney appears twice). *team* wouldn't be a good choice *Manchester United* appears twice. So in this table we could specify a composite primary key (**name** and **team**). The combination of these two attributes identifies the row.
> Even this might not be future proof as eventually there are going to be two different players with the same name that have played for the same team. So we would probably use a surrogate key.
