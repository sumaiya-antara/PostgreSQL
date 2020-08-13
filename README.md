# PostgreSQL

## What is PostgreSQL
PostgreSQL, also known as Postgres, is a free and open-source relational database management system emphasizing extensibility and SQL compliance.

* Datagrip- paid and powerful
* Postico- free and for mac use
* pgAdmin- for windows and free


*******postgres is the default super user
***Postgresql installation in windows:

use sql shell****
default port for postgresql=5432

***Create Database:
Commands:

psql
\l
\l
CREATE DATABASE test;
\l

***Connect Database:
Commands:

psql --help
psql -h localhost -p 5432 -U amigoscode 

\q
psql
\l
\c test
\c amigoscode
\c test

***A very dangerous command:
DROP DATABASE test;
------------------Beware of using DROP command-------

**********Create table without constraint:
Command:
psql

\c


> CREATE TABLE person (
> id INT;
> first_name VARCHAR(50),
> last_name VARCHAR(50),
> email VARCHAR(150) );

 
 

\d person


****Insert into:

INSERT INTO person (first_name, last_name, gender, date_of_birth)
VALUES ('Anne', 'Smith', 'FEMALE', date '1988-01-09');

INSERT INTO person (first_name, last_name, gender, date_of_birth, email)
VALUES ('Jake', 'Gillenhal', 'MALE', date '1982-05-23', 'jake@gmail.com');


*****Generate 1000 rows with Mockaroo:

Commands:
psql
SELECT * FROM person;

-------Download 1000 rows of data from mockaroo

Use Atom, Sublime, VSCODE


********Take data from file to cli:
command:
\i /path

 
***Select from:

SELECT * FROM person;
SELECT FROM person; (it will show no data)
SELECT first_name FROM person;
SELECT first_name, second_name FROM person;
SELECT email FROM person;




\d person

**********Create table with constraint:
 
CREATE TABLE person (
id BIGSERIAL NOT NULL PRIMARY KEY,
first_name VARCHAR(50) NOT NULL,
last_name VARCHAR(50) NOT NULL,
gender VARCHAR(7) NOT NULL,
date_of_birth DATE NOT NULL,
email VARCHAR(150) );


***Order by:
SELECT * FROM person ORDER BY country_of_birth ASC;
SELECT * FROM person ORDER BY country_of_birth DESC;
SELECT * FROM person ORDER BY id ASC;
SELECT * FROM person ORDER BY first_name;
 
SELECT * FROM person ORDER BY id, email;


***Distinct:

SELECT DISTINCT country_of_birth FROM person ORDER BY country_of_birth;
SELECT DISTINCT country_of_birth FROM person ORDER BY country_of_birth DESC;


***Where clause and AND:

SELECT * FROM person WHERE gender = 'Female';
SELECT * FROM person WHERE gender = 'Male' AND country_of_birth = 'China';
SELECT * FROM person WHERE gender = 'Female' AND (country_of_birth = 'China' OR country_of_birth = 'Poland');
SELECT * FROM person WHERE gender = 'Female' AND (country_of_birth = 'China' OR country_of_birth = 'Poland')
AND last_name = 'Pietersma';


*******Comparison:

SELECT 1>=2;
SELECT 1=2;
SELECT 1<=1;
SELECT 1 <> 2;
SELECT 'PRESENT' = 'present';
SELECT 'PRESENT' = 'PRESENT';
SELECT 'PRESENT' = 'PRESENTS';

****Limit, Offset and Fetch:

SELECT * FROM person LIMIT 15;
SELECT * FROM person OFFSET 15 LIMIT 15;
SELECT * FROM person OFFSET 15;
SELECT * FROM person OFFSET 15 FETCH FIRST 10 ROW ONLY;


******IN:

SELECT * FROM person WHERE country_of_birth IN ('China', 'France', 'Portugal');
SELECT * FROM person WHERE country_of_birth IN ('China', 'France', 'Portugal') ORDER BY country_of_birth;

****Between:

SELECT * FROM person WHERE date_of_birth BETWEEN DATE '2020-01-01' AND '2020-06-11';

*******LIKE & ILIKE :

SELECT * FROM person WHERE email LIKE '%.com';
SELECT * FROM person WHERE email LIKE '%@boston.com';
SELECT * FROM person WHERE email LIKE '%@google.%';
SELECT * FROM person WHERE email LIKE '______@%';
SELECT * FROM person WHERE email LIKE '______a@%';
SELECT * FROM person WHERE country_of_birth LIKE 'F%';

SELECT * FROM person WHERE country_of_birth LIKE 'f%';  -----this command will show nothing
SELECT * FROM person WHERE country_of_birth ILIKE 'f%';










