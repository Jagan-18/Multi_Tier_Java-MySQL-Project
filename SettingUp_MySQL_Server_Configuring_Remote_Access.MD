Setting Up MySQL Server and Configuring Remote Access
1. Install MySQL Server:

```
sudo apt update
sudo apt install mysql-server -y
```
2. Access MySQL as Root:
```
sudo mysql -u root
```
- When we are Running next time we need to give command: 
 ```
 sudo mysql -u root -p
 ```

3. Set Root User Password:
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Test@123';
```
- After Running above command some Change to be done backend.
```
FLUSH PRIVILEGES;
```
4. Create a Database:
```
CREATE DATABASE bankappdb;
```
1. If case we want to View databases inside:
 - show databases;

 #### Output:
 Database           |
+--------------------+
| bankappdb          |
| information_schema |
| mysql              |
| performance_schema |
| sys 

2. you wamt to see the bankappdb date files.
- USE bankappdb;   # O/P: Database changed
- show tables;  # Output: empty set
exit;


#_____________________#
## Install Maven and java
```
sudo apt install openjdk-17-jdk-headless -y
sudo apt install maven -y

```
1. mvn package

2. Next change dir to traget ( cd traget/)
  - java -jar bankapp-0.0.1-SNAPSHOT.jar  # It will created on temper tomcat server and run on port 8080
3. Take IP Address and open brower with the Port 8080
- Public IPv4 address:8008

5. Modify MySQL Configuration for Remote Access:
o Open the MySQL configuration file:

```
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
o Locate the line:
 - bind-address = 127.0.0.1
o Change it to:
 - bind-address = 0.0.0.0

o Save and exit (Ctrl+O, Enter, Ctrl+X).

6. Restart MySQL Service:
```
sudo systemctl restart mysql
```
7. Verify MySQL is Listening on Port 3306:
```
sudo netstat -tuln | grep 3306
```
8. Create a New User with Remote Access:
o Log back into MySQL:
```
sudo mysql -u root -p
```
o Create a new user and grant privileges:
```
CREATE USER 'dev'@'%' IDENTIFIED BY 'dev';
GRANT ALL PRIVILEGES ON *.* TO 'dev'@'%';
FLUSH PRIVILEGES;
exit;
```
Accessing the Database via phpMyAdmin
1. Go to phpMyAdmin Online.
2. Enter the following details:
o Host: Public IP address of the MySQL server.
o Username: dev
o Password: dev
o Database: Leave empty or specify bankappdb.
3. Connect to manage the database.
Important Notes:
• Ensure that the firewall allows incoming traffic on port 3306. For example:
```
sudo ufw allow 3306
```
• It's highly recommended to use strong passwords and secure configurations for production 
environments.
• Restrict IP access in MySQL if possible to avoid exposing the database to all IPs (%).
This document ensures a functional setup and remote access to your MySQL server for your project