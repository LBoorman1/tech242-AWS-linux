# App VM Script
```
#!/bin/bash

#Update and upgrade
sudo DEBIAN_FRONTEND=noninteractive apt update -y
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y

#Install relevant packages
sudo DEBIAN_FRONTEND=noninteractive apt install mysql-client -y
sudo DEBIAN_FRONTEND=noninteractive apt install maven -y
sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y
sudo DEBIAN_FRONTEND=noninteractive apt install git -y

#Fresh clone of the repo
cd ~
rm -rf repo
git clone https://github.com/LBoorman1/tech242-luke-world-repository.git ~/repo

db_ip=

cd repo/WorldProject

#Set environment variables
export DB_HOST=jdbc:mysql://$db_ip:3306/world
export DB_USER=root
export DB_PASS=root


#Check mySQL connection and if successful, run the app
output=$(mysql -h $db_ip -u root -proot -e "USE world; SELECT 1" 2>&1)
if [ $? -eq 0 ]; then
    echo "Connected Successfully"
    mvn clean package spring-boot:start
else
    echo "Failed to connect"
    echo $output
fi

#Setting up the reverse proxy
sudo DEBIAN_FRONTEND=noninteractive apt install -y apache2

sudo systemctl enable apache2


sudo a2enmod proxy
sudo a2enmod proxy_http

config_file="/etc/apache2/sites-available/000-default.conf"

if ! grep -q "ProxyPass / http://localhost:5000/" "$config_file"; then
    sudo sed -i '/<\/VirtualHost>/i\    ProxyPass / http:\/\/localhost:5000/' ">
fi

if ! grep -q "ProxyPassReverse / http://localhost:5000/" "$config_file"; then
    sudo sed -i '/<\/VirtualHost>/i\    ProxyPassReverse / http:\/\/localhost:5>
fi

if ! grep -q "ProxyPreserveHost On" "$config_file"; then
    sudo sed -i '/<\/VirtualHost>/i\    ProxyPreserveHost On' "$config_file"
fi

sudo systemctl reload apache2
```

The if statement here allows the `mysql -h` command to provide an exit status of 0 if successful, therefore
the script can check if there is an appropriate database connection.