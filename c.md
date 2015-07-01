### Installing mysql
Enter https://help.ubuntu.com/12.04/serverguide/mysql.html#mysql-installation
Run sudo apt-get install mysql-server into Terminal
Create password : nuuts (which means secret in mongolian)

### Begin
Started following/reading instructions from http://dev.mysql.com/doc/refman/5.7/en/database-use.html
use "/usr/bin/mysql -u root -p" to start using mysql

## Lookup for users
SELECT User, Host, Password FROM mysql.user;

## Create Database
CREATE DATABASE tz;
USE tz
QUIT tz
# Delete Database
DROP DATABASE <~>;

## Add Database User
INSERT INTO mysql.user (User,Host,Password) VALUES('Tegshig','localhost',PASSWORD('demopassword'));
Make MySQL read changes through "FLUSH PRIVILEGES;"
Grant data base user permissions through "GRANT ALL PRIVILEGES ON tz.* to tegshig@localhost;"
Make MySQL read changes through "FLUSH PRIVILEGES;"

## Check privileges 
SHOW GRANTS FOR 'tegshig'@'localhost';

## Change password of database user Tegshig
UPDATE mysql.user SET Password = PASSWORD('nuuts') WHERE User = 'tegshig';
This must be done through root (user)

## Create Table
# Student
create table student (name VARCHAR(20), id VARCHAR(20), firstname VARCHAR(20), lastname VARCHAR(20), birthday DATE);
# Address
create table address (id VARCHAR(20),user_id VARCHAR(20), street VARCHAR(20), town VARCHAR(20), zip VARCHAR(20));
# Delete Column in Table
ALTER table student
    -> drop column name;

## Add Data into Tables
INSERT INTO pet
VALUES ('Puffball','Diane','hamster','f','1999-03-30',NULL);

#Change Column name
ALTER TABLE address CHANGE town country INT;
#Change colum definition
ALTER TABLE address MODIFY COLUMN country VARCHAR(20);

