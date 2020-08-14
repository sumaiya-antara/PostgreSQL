# PostgreSQL

## What is PostgreSQL
PostgreSQL which is also known as Postgres, is a free and open-source relational database management system developed by a worldwide team of volunteers. It is claimed to be the most advanced open source database solution. It provides an implementation of the SQL querying language. It runs on several platforms including Linux, UNIX, Mac OS X, Windows, True64 and Solaris.

This documentation demonstrates the installation of Postgresql on Windows 10 Pro and instructions for basic database administartion along with mentioning the key basics. The possible problems you can face while executing the administration, will also be mentioned.

## Step 1: Installation of PostgreSQL on Windows 10 pro
At first,download the PostgreSQL from https://www.postgresql.org/. For downloading, follow the below steps:

1. Go to postgresql.org
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

postgres=#
```

#### Important Notes:
- The default Superuser for PostgreSQL is **postgres**
- The defualt port for PostgreSQL is **5432**

## Step 2: Creating Database:

Create a database by simply logging into the superuser **postgres** and writing the following command:
```
CREATE DATABASE test
```
Check the List of Databases with the command **\l**.
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





















