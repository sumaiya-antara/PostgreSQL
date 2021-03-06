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
#### Important Note:
Provide the value/select the value for DATE variable in the **yyyy-mm-dd** format. Otherwise, the operations may fail showing the following errors:

![error](https://user-images.githubusercontent.com/33460747/90296988-fc7dcc80-deae-11ea-86f0-159f5ba735ca.PNG)

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
We can select separate columns specifically with the help of a DISTINCT operator. The following command will show the data of a single column only-
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

![p9](https://user-images.githubusercontent.com/33460747/90297086-38b12d00-deaf-11ea-90ec-d1819dbc07c0.PNG)
![p10](https://user-images.githubusercontent.com/33460747/90297089-3949c380-deaf-11ea-80b3-b91ff5fa35d4.PNG)
![p11](https://user-images.githubusercontent.com/33460747/90297090-39e25a00-deaf-11ea-9f74-0dd99f7a92d9.PNG)

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


#### GROUP BY:
The GROUP BY clause allows to group our data based on column. For example, we want to see the number of persons from each country from the **person** table. Execute the following queries for this operation:
```
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth;
```
This command will display country names with the number of person from each of those countries.

The Output:

![group by](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/group%20by.PNG)



```
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth ORDER BY country_of_birth;
```

This command will display country names along with total number of persons from those in an order.

The Output:

![group by](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/group%20by2.PNG)


## GROUP BY HAVING:
The **GROUP BY HAVING** clause allows to do an extra filtering after we perform the aggregation(such as **count**). The **HAVING** keyword works with **GROUP BY**. Suppose, we need to find out the country names having at least/at most 5 people and number of people from those countries in the table. Then we will perform the following queries:

```
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth HAVING COUNT(*) <3 ORDER BY country_of_birth;
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth HAVING COUNT(*) >50 ORDER BY country_of_birth;
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth HAVING COUNT(*) >=100 ORDER BY country_of_birth;
```

OUTPUTS:

![group by having](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/group%20by%20having.PNG)
![group by having 2](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/group%20by%20having%202.PNG)


###### NOTES: 
- You must place the **HAVING** keyword before **ORDER BY**.
- **COUNT(*)** is an aggregate function. 
An aggregate function performs a calculation on a set of values, and returns a single value. Except for COUNT(*), aggregate functions ignore null values. Aggregate functions are often used with the **GROUP BY** clause of the **SELECT** statement.
Use aggregate functions as expressions only in the following situations:

- The select list of a SELECT statement (either a subquery or an outer query).
- A HAVING clause.

Transact-SQL provides the following aggregate functions:

- APPROX_COUNT_DISTINCT
- AVG
- CHECKSUM_AGG
- COUNT
- COUNT_BIG
- GROUPING
- GROUPING_ID
- MAX
- MIN
- STDEVP
- STRING_AGG
- SUM
- VAR
- VARP



## Calculating MAX,MIN and AVERAGE:
Suppose we have another table named car in the test database and this table has id, make, model, price columns.
If we want to see the Maximum, Minimum and Average price of the cars in the table, let's perform the following queries.

```
SELECT MAX(price) FROM car;
SELECT MIN(price) FROM car;
SELECT AVG(price) FROM car;
SELECT ROUND(AVG(price)) FROM car;
SELECT make,model, MIN(PRICE) FROM car GROUP BY make,model;
SELECT make,MAX(PRICE) FROM car GROUP BY make;
SELECT make,AVG(PRICE) FROM car GROUP BY make;
SELECT make,ROUND(AVG(PRICE)) FROM car GROUP BY make;
```
OUTPUTS:

![mmma1](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/mma1.PNG)
![mmma1](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/mma2.PNG)
![mmma1](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/mma3.PNG)
![mmma1](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/mma4.PNG)


###### NOTE:
The PostgreSQL ROUND() function rounds a numeric value to its nearest integer or a number with the number of decimal places.


## SUM:
```
SELECT SUM(price) FROM car;
SELECT make, model, SUM(price) FROM car GROUP BY make, model;
```

This query will show the total price of all the cars of each model from every brand.

![sum1](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/Sum1.PNG)
![sum2](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/sum2.PNG)


## Basic Arithmetic Operators:
```
SELECT 10 + 2;
SELECT 25 - 14;
SELECT 8 * 4;
SELECT 55 / 11;
SELECT 5 ^ 3;
SELECT 6!;
SELECT 20 % 7;
```
## Arithmetic Operator ROUND:
Suppose, 10% discount is going on for the cars.Let's view the discount amount and the discounted price of each cars in the car table.
```
SELECT id, make, model, price, price * .10 FROM car;
SELECT id, make, model, price, ROUND(price * .10) FROM car;
```

This command will display the discount amount of each car models in the round column.

![round1](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/arround1.PNG)
![round2](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/arround2.PNG)

```
SELECT id, make, model, price, ROUND(price * .10, 2) FROM car;
```
This query will show 2 digited decimal number of the discount amount.

![round3](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/arround3.PNG)

```
SELECT id, make, model, price, ROUND(price * .10, 2), ROUND(price - (price * 0.10), 2) FROM car;
```
This query will show the discounted price of each car models along with discount amount and the original price of the cars.

![round4](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/arround4.PNG)




## ALIAS:

If we do not specify the column name in PostgreSQL, the function name will displayed as the column name. We need use Alias to specify a column name. We simply need to use the AS keyword and then the column_name. For the previous query, let's perform the following actions:

```
SELECT id, make, model, price AS original_price, ROUND(price * .10, 2) AS discount_amount_for_ten_percent, ROUND(price - (price * 0.10), 2) AS price_after_ten_percent_discount FROM car;
```
Output:

![alias](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/alias1.PNG)


## COALESCE:
The COALESCE function accepts an unlimited number of arguments. It returns the first argument that is not null. If all arguments are null, the COALESCE function will return null.

Suppose, there is another table named person2 in my database test and many of the persons do not have email address. Let's see what COALESCE function does in this scenario.

```
SELECT COALESCE(email) FROM person2;
```
Output:

![coalesce](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/coalesce1.PNG)


The output of this query is showing the NOT NULL values (email addresses) from the email column. But, the default NULL values are aslso being printed as blank.
Let's print this default NULL values with a string.

```
SELECT COALESCE(email, '***EMAIL NOT PROVIDED***') FROM person2;
```

Output:

![c2](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/coalesce2.PNG)

## NULLIF:
The NULLIF function returns NULL if and only if value1 and value2 are equal. Otherwise it returns value1. This can be used to perform the inverse operation of the COALESCE example given above.
PostgreSQL nullif is a common conditional expression used to handle null values or expressions in PostgreSQL. nullif also used with the coalesce function to handle the null values. PostgreSQL nullif function returns a null value if provided expressions are equal. If two expressions provided are equal then it provides null value as a result otherwise it will return the first expression as a result.

```
SELECT NULLIF(20 , 5);
SELECT NULLIF(20 , 20);
SELECT NULLIF(2 , 8);
SELECT 10 / NULLIF(2 , 6);
SELECT COALESCE(10 / NULLIF(0 , 0),0);
```
It will print the output 0.

```
SELECT first_name, last_name, COALESCE(email , 'NOT FOUND') AS email FROM person2;
```
OUTPUT:

![NULLIF](https://github.com/sumaiya-antara/PostgreSQL/blob/master/PostgreSQL/nullif1.PNG)


## :
```
SELECT NOW();
SELECT NOW()::DATE;
SELECT NOW()::TIME;
```

## Adding and Subtracting with Dates:
```
SELECT NOW() - INTERVAL '2 YEARS';
SELECT NOW() - INTERVAL '7 MONTHS';
SELECT NOW() - INTERVAL '7 DAYS';
SELECT NOW() + INTERVAL '7 DAYS';
SELECT NOW()::DATE + INTERVAL '8 MONTHS';
SELECT (NOW()::DATE + INTERVAL '8 MONTHS')::DATE;
```
























































