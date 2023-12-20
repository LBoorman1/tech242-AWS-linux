# Script for the database vm
needs security group ssh my ip and MySQL on port 3306
```
#!/bin/bash

#Update and upgrade packages
sudo DEBIAN_FRONTEND=noninteractive apt update -y
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y


#set username and password as root
sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
sudo apt-get update

#install mysql
sudo DEBIAN_FRONTEND=noninteractive apt install -y mysql-server

#Enable MySQL server
sudo systemctl enable mysql

#configures the mysql
config_file="/etc/mysql/mysql.conf.d/mysqld.cnf"
sudo sed -i 's/^bind-address\s*=.*$/bind-address = 0.0.0.0/' $config_file
sudo systemctl restart mysql

#Download the SQL script from the github repo
wget https://raw.githubusercontent.com/LBoorman1/tech242-luke-world-repository/main/world.sql

#Run the SQL script
sudo mysql -u root -proot < world.sql

#Creates the root user that can be accessed from anywhere
sudo mysql -u root -proot -e "CREATE USER IF NOT EXISTS 'root'@'%' IDENTIFIED BY 'root'; GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION; FLUSH PRIVILEGES;"
```