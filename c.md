	MYSQL
====================

### Installing mysql
Enter https://help.ubuntu.com/12.04/serverguide/mysql.html#mysql-installation
Run sudo apt-get install mysql-server into Terminal
Create password : nuuts (which means secret in mongolian)

### Begin
Started following/reading instructions from http://dev.mysql.com/doc/refman/5.7/en/database-use.html
use >"/usr/bin/mysql -u root -p" to start using mysql

## Lookup for users
>SELECT User, Host, Password FROM mysql.user;

## Create Database
>CREATE DATABASE tz;
>USE tz
QUIT tz
# Delete Database
>DROP DATABASE <~>;

## Add Database User
>INSERT INTO mysql.user (User,Host,Password) VALUES('Tegshig','localhost',PASSWORD('demopassword'));
Make MySQL read changes through >"FLUSH PRIVILEGES;"
Grant data base user permissions through >"GRANT ALL PRIVILEGES ON tz.* to tegshig@localhost;"
Make MySQL read changes through >"FLUSH PRIVILEGES;"

## Check privileges 
>SHOW GRANTS FOR 'tegshig'@'localhost';

## Change password of database user Tegshig
>UPDATE mysql.user SET Password = PASSWORD('nuuts') WHERE User = 'tegshig';
This must be done through root (user)

## Create Table
# Student
>CREATE TABLE student (name VARCHAR(20), id VARCHAR(20), firstname VARCHAR(20), lastname VARCHAR(20), birthday DATE);
# Address
>CREATE TABLE address (id VARCHAR(20),user_id VARCHAR(20), street VARCHAR(20), town VARCHAR(20), zip VARCHAR(20));
# Delete Column in Table
>ALTER TABLE student DROP COLUMN name;

## Add Data into Tables
>INSERT INTO pet VALUES ('Puffball','Diane','hamster','f','1999-03-30',NULL);
Another Option Load a file
# Change Column name
>ALTER TABLE address CHANGE town country INT;
# Change colum definition
>ALTER TABLE address MODIFY COLUMN country VARCHAR(20);

## Delete Data from Table
# Delete query
>DELETE FROM address WHERE country = "Saale"
# Change single query 
>UPDATE address SET country = "England" WHERE street = "London";

### Retrieve Information
SELECT what_to_select
FROM which_table
WHERE conditions_to_satisfy;
## Show Table
SELECT * FROM <Table_Name>
# Operators
AND
OR
>SELECT * FROM pet WHERE (species = 'cat' AND sex = 'm') OR (species = 'dog' AND sex = 'f'); // for rows where these conditions apply
# Rows
>SELECT * FROM pet WHERE name = 'Bowser';
# Columns
>SELECT name, birth FROM pet;
>SELECT DISTINCT owner FROM pet; //for each unique output

## Sort
# Sorting Rows
>SELECT name, birth FROM pet ORDER BY birth; 		// sorted by date (ascending)
>SELECT name, birth FROM pet ORDER BY birth DESC; 	// sorted by date (descending)
>SELECT name, species, birth FROM pet ORDER BY species, birth DESC;	multiple columns,type of animal ascending, birth date descending

## Date
# Show Age
>SELECT firstname, TIMESTAMPDIFF(YEAR,BIRTHDAY,CURDATE()) AS age FROM student;	//given in years from birthday until curdate()
# Show Difference between 2 Dates
>SELECT name, birth, death, TIMESTAMPDIFF(YEAR,birth,death) AS age FROM pet WHERE death IS NOT NULL ORDER BY age; // is not null

>SELECT firstname, TIMESTAMPDIFF(YEAR,birthday,CURDATE()) AS age, YEAR(birthday), YEAR(CURDATE()) FROM student ORDER BY age;

## Pattern matching
# Like
>SELECT firstname FROM student WHERE firstname LIKE "T%";
# Regexp
>SELECT * FROM pet WHERE name REGEXP '^.{5}$'; // n times . which causes to create 5 dots which represents the name

## Counting rows
>SELECT owner, COUNT(*) FROM pet GROUP BY owner // how many pets does one unique owner have (distinctive)
f.e. SELECT species, sex, COUNT(*) FROM pet WHERE sex IS NOT NULL GROUP BY species, sex;

## Multiple Tables in a Database
>SELECT student.lastname, address.town FROM student INNER JOIN address ON student.id = address.id // inner join on this condition , where

