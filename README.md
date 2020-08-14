# PostgreSQL

## What is PostgreSQL
PostgreSQL which is also known as Postgres, is a free and open-source relational database management system developed by a worldwide team of volunteers. It is claimed to be the most advanced open source database solution. It provides an implementation of the SQL querying language. It runs on several platforms including Linux, UNIX, Mac OS X, Windows, True64 and Solaris.

This documentation demonstrates the installation of Postgresql on Windows 10 Pro and instructions for basic database administartion along with mentioning the key basics. The possible problems you can face while executing the administration, will also be mentioned.

## Installation of PostgreSQL on Windows 10 pro
At first,download the PostgreSQL from https://www.postgresql.org/. For downloading, follow the below steps:

1. Go to www.postgresql.org
2. Click on Download
3. Click on Windows 
4. Click on Download the Installer 
5. Download the desired version as per your System Type(64 bit or 32 bit)

After downloading, complete the setup of the downloaded .exe file just like any other programs. Provide a password for **Superuser** while doing the setup and remember this password must. Finish the setup. A SQL Shell(psql) and a graphical user interface pgAdmin4 will be installed for operating the database. In this demonstartion, using of SQL Shell(psql) will be in focus.
Click the psql application to launch it. The psql command-line program will display. Enter all the necessary information such as the server, database, port, username, and password. To accept the default, press Enter. Provide the password that you entered during installing the PostgreSQL.

```
Server [localhost]:
Database [postgres]:
Port [5432]:
Username [postgres]:
Password for user postgres:
psql (11.8)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

```

#### Important Notes:
- The default Superuser for PostgreSQL is **postgres**
- The defualt port for PostgreSQL is **5432**

## Creating Database:

- Create a database by simply logging into the superuser **postgres** and writing the query **CREATE DATABASE database_name;** (put the name of the database in the database_name section and put a semicolon (;) at the end of the command for must.
```
Example:

CREATE DATABASE test;
```

- Check the List of Databases with the command **\l**
```
postgres-# \l
                                                 List of databases
   Name    |  Owner   | Encoding |          Collate           |           Ctype            |   Access privileges
-----------+----------+----------+----------------------------+----------------------------+-----------------------
 postgres  | postgres | UTF8     | English_United States.1252 | English_United States.1252 |
 template0 | postgres | UTF8     | English_United States.1252 | English_United States.1252 | =c/postgres          +
           |          |          |                            |                            | postgres=CTc/postgres
 template1 | postgres | UTF8     | English_United States.1252 | English_United States.1252 | =c/postgres          +
           |          |          |                            |                            | postgres=CTc/postgres
 test      | postgres | UTF8     | English_United States.1252 | English_United States.1252 |
(4 rows)
```

- A whole Database can be deleted with DROP command.
```
Example:

DROP DATABASE test;
```


#### Important Notes:
- UPPERCASE letters and LOWERCASE letters both can be used while writing database queries
- Putting semicolon (;)  at the end of the query is a must. Otherwise, the query will not be executed
- BEAWARE before executing any DROP query because it will delee the database forever


## Connect to Database:
To connect with any database, start with writing **\c** and then write the database name.

```
Example:
postgres-# \c test
You are now connected to database "test" as user "postgres".
```

## Create Table without Constraint:
Constraints are the rules enforced on data columns on table and these are used to prevent invalid data from being entered into the database. This ensures the accuracy and reliability of the data in the database.
Some of the commonly used constraints in PostgreSQL are:

- NOT NULL Constraint: Ensures that a column cannot have a NULL value.

- UNIQUE Constraint: Ensures that all values in a column are different.

- PRIMARY Key: Uniquely identifies each row/record in a database table.

- FOREIGN Key: Constrains data based on columns in other tables.

- CHECK Constraint: The CHECK constraint ensures that all values in a column satisfy certain conditions.

- EXCLUSION Constraint: The EXCLUDE constraint ensures that if any two rows are compared on the specified column(s) or expression(s) using the specified operator(s), not all of these comparisons will return TRUE.

```
Example:
test=# CREATE TABLE people (
test(# id INT,
test(# first_name VARCHAR(50),
test(# last_name VARCHAR(50),
test(# gender VARCHAR(7),
test(# date_of_birth DATE,
test(# email VARCHAR(150) );
CREATE TABLE

test=#  \d
              List of relations
 Schema |     Name      |   Type   |  Owner
--------+---------------+----------+----------
 public | ant           | table    | postgres
 public | faisal        | table    | postgres
 public | people        | table    | postgres
 public | person        | table    | postgres
 public | person_id_seq | sequence | postgres
 public | tasmi         | table    | postgres
(6 rows)
```

## Create Table with Constraint:
For creating table with constraint, type the following queries in the SQL shell:
```
CREATE TABLE person (
id BIGSERIAL NOT NULL PRIMARY KEY,
first_name VARCHAR(50) NOT NULL,
last_name VARCHAR(50) NOT NULL,
gender VARCHAR(7) NOT NULL,
date_of_birth DATE NOT NULL,
email VARCHAR(150) );
```
Then check the table with **\d** command
![p8](https://user-images.githubusercontent.com/33460747/90296122-86786600-deac-11ea-8c48-63469f84410c.PNG)

## SELECT Operations:
The PostgreSQL SELECT statement is used to retrieve records from one or more tables of database and the data is returned in the form of a result table. The SELECT command contains several clauses that we can use to write a query easily. The basic task while performing the SELECT command is to query data from tables within the database. The different clauses of SELECT command are discussed below:
#### ORDER BY:
We can sort the rows of tables with the help of the ORDER BY clause.

The data from person table can be sorted according to their country of birth with the following command/query:

```
SELECT * FROM person ORDER BY country_of_birth;
```
The data from person table can be sorted according to their id with the following command/query:
```
SELECT * FROM person ORDER BY id;
```
The data from any table can be sorted in ascending or descending order with **ASC** or **DSC** at the end of the query.
```
Example:
SELECT * FROM person ORDER BY country_of_birth ASC;
SELECT * FROM person ORDER BY country_of_birth DESC;
SELECT * FROM person ORDER BY id ASC;
```

#### DISTINCT:
We can select separate rows with the help of a DISTINCT operator.
```
SELECT DISTINCT country_of_birth FROM person ORDER BY country_of_birth;
```
The output:

![p20](https://user-images.githubusercontent.com/33460747/90296227-bfb0d600-deac-11ea-8b39-637d9a784b55.PNG)

#### WHERE Clause:
We can filter the rows with the help of the WHERE clause.
```
SELECT * FROM person WHERE gender = 'Female';
```

#### WHERE and AND Clause:
We can filter the rows with multiple options by using the WHERE and AND clause.
```
SELECT * FROM person WHERE gender = 'Male' AND country_of_birth = 'China';
SELECT * FROM person WHERE gender = 'Female' AND (country_of_birth = 'China' OR country_of_birth = 'Poland');
SELECT * FROM person WHERE gender = 'Female' AND (country_of_birth = 'China' OR country_of_birth = 'Poland') AND last_name = 'Pietersma';
```

#### Comparison:
We can simply perform comparisons with **>,<,=** opertaors and see the output in true or false.
```
SELECT 1>=2;
SELECT 1=2;
SELECT 1<=1;
SELECT 1 <> 2;
SELECT 'PRESENT' = 'present';
SELECT 'PRESENT' = 'PRESENT';
SELECT 'PRESENT' = 'PRESENTS';
```

#### INSERT INTO:
For inserting data into any table, use the INSERT INTO clause. Follow the below example:
```
INSERT INTO person (first_name, last_name, gender, date_of_birth)
VALUES ('Anne', 'Smith', 'FEMALE', date '1988-01-09');

INSERT INTO person (first_name, last_name, gender, date_of_birth, email)
VALUES ('Jake', 'Gillenhal', 'MALE', date '1982-05-23', 'jake@gmail.com');
```
###### Important Notes:
We can generate data by using mockaroo data generator for performing and checking the database queries. We need a large number of data for performing the database quieries and it is a lengthy process to insert data one by one and then test those with quiery. Go to [mockaroo](https://www.mockaroo.com/) for generating your data and the download the .sql file. Open the file using any code editor like Atom, Sublime, VSCODE etc.

Insert the file's data to the table by executing commands like this:
```
test=# \i /Users/ttsta/Downloads/person.sql
INSERT 0 1
INSERT 0 1
INSERT 0 1
INSERT 0 1
.
.
.
```


#### LIMIT, OFFSET and FETCH:
We can view a fixed limited number of data from the table by using LIMIT operation.
```
SELECT * FROM person LIMIT 15;
```
The above command will display the first 15 data from the table. For viewing data from a specific number with a limit, use the OFFSET operation.
Follow the below command for this:
```
SELECT * FROM person OFFSET 15 LIMIT 15;
```
We can also use the OFFSET command for viewing the rest of the data from a specific serial.
```
SELECT * FROM person OFFSET 15;
```
The FETCH operation can be used instead of LIMIT for displaying data from a specific serial.
```
SELECT * FROM person OFFSET 15 FETCH FIRST 13 ROW ONLY;
```

#### LIKE and ILIKE:
The PostgreSQL LIKE operator is used query data using pattern matching techniques. Its result include strings that are case-sensitive and follow the mentioned pattern.
It is important to know that PostgreSQL provides with 2 special wildcard characters for the purpose of patterns matching as below:

- Percent ( %) for matching any sequence of characters
- Underscore ( _ ) for matching any single character

Suppose, we want to find out all the data of person table who has the email id with .com.
Execute the following command:
```
SELECT * FROM person WHERE email LIKE '%.com';
```
This command will show the below result:
![p31](https://user-images.githubusercontent.com/33460747/90294745-fab10a80-dea8-11ea-94c5-405ebb2cc9e8.PNG)

Some more example queries and their outputs are provided below:
```
Query:
SELECT * FROM person WHERE email LIKE '%@jigsy.com';
```
Result:

![p32](https://user-images.githubusercontent.com/33460747/90294883-5c717480-dea9-11ea-86fb-00e5c1fc8646.PNG)

```
Query:
SELECT * FROM person WHERE email LIKE '%@google.%';
```
Result:

![p33](https://user-images.githubusercontent.com/33460747/90294923-714e0800-dea9-11ea-98f8-830743165927.PNG)

```
Query:
SELECT * FROM person WHERE email LIKE '______@%';
```
Result:

![p34](https://user-images.githubusercontent.com/33460747/90294945-7e6af700-dea9-11ea-8a68-335300cf7c0e.PNG)

Some more queries are:
```
SELECT * FROM person WHERE country_of_birth LIKE 'F%';

SELECT * FROM person WHERE country_of_birth LIKE 'f%';
```

###### Note:
- LIKE and ILIKE are used for pattern matching in PostgreSQL. LIKE is the SQL standard while ILIKE is a useful extension made by PostgreSQL
- ILIKE is similar to LIKE in all aspects except in one thing. It performs a case in-sensitive matching.
```
Example:
SELECT * FROM person WHERE country_of_birth ILIKE 'f%';
```

#### IN:
The PostgreSQL IN condition is used to help reduce the use of multiple OR conditions in a SELECT, INSERT, UPDATE, or DELETE statement.
```
Example:
SELECT * FROM person WHERE country_of_birth IN ('China', 'France', 'Portugal');
SELECT * FROM person WHERE country_of_birth IN ('China', 'France', 'Portugal') ORDER BY country_of_birth;
```

#### BETWEEN:
The PostgreSQL BETWEEN condition is used to retrieve values within a range in a SELECT, INSERT, UPDATE or DELETE statement.
```
Example:
SELECT * FROM person WHERE date_of_birth BETWEEN DATE '2020-01-01' AND '2020-06-11';
```
This query will show the data of persons who was born between the dates 2020-01-01 and 2020-06-11.


















































