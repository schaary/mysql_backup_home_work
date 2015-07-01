### Installing mysql
Enter https://help.ubuntu.com/12.04/serverguide/mysql.html#mysql-installation
Run sudo apt-get install mysql-server into Terminal
Create password : nuuts (which means secret in mongolian)

## Begin

Started following/reading instructions from http://dev.mysql.com/doc/refman/5.7/en/database-use.html
use "/usr/bin/mysql -u root -p" to start using mysql

# Create Database

CREATE DATABASE tzstudent;
USE tzstudent
QUIT tzstudent

# Add Database User

INSERT INTO mysql.user (User,Host,Password) VALUES('Tegshig','localhost',PASSWORD('demopassword'));
Make MySQL read changes through "FLUSH PRIVILEGES;"
Grant data base user permissions through "GRANT ALL PRIVILEGES ON tz.* to tegshig@localhost;"
Make MySQL read changes through "FLUSH PRIVILEGES;"

# Check privileges 
SHOW GRANTS FOR 'tegshig'@'localhost';

# Change password of database user Tegshig

UPDATE mysql.user SET Password = PASSWORD('nuuts') WHERE User = 'tegshig';
This must be done through root (user)
