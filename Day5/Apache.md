```
#!/bin/bash

#update and upgrade
sudo DEBIAN_FRONTEND=noninteractive apt update -y
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y

#install maven
sudo DEBIAN_FRONTEND=noninteractive apt install -y maven

#install jdk (java) 17
sudo DEBIAN_FRONTEND=noninteractive apt install -y openjdk-17-jdk

#install git
sudo DEBIAN_FRONTEND=noninteractive apt install git

#delete repo from remote if exists
cd ~
rm -rf repo

#copy the app code to the VM
git clone https://github.com/LBoorman1/tech242-jsonvoorhees-app.git ~/repo

#cd to proper directory
cd ~/repo/springapi

#start the application
mvn spring-boot:start

DOMAIN=$(curl ifconfig.me)
TARGET_IP=$(curl ifconfig.me)
TARGET_PORT="5000"

sudo DEBIAN_FRONTEND=noninteractive apt install -y apache2
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_balancer
sudo a2enmod lbmethod_byrequests

sudo tee /etc/apache2/sites-available/reverse-proxy.conf > /dev/null <<EOL
<VirtualHost *:80>
    ServerName $DOMAIN

    ProxyPreserveHost On
    ProxyPass / http://$TARGET_IP:$TARGET_PORT/
    ProxyPassReverse / http://$TARGET_IP:$TARGET_PORT/

    ErrorLog \${APACHE_LOG_DIR}/error.log
    CustomLog \${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
EOL

sudo a2ensite reverse-proxy

sudo systemctl reload apache2
```

This script allows the server to use apache to configure a reverse-proxy so that when
users visit the given ip address, they are redirected to the port 5000.

The script also gets the public Ip address of the instance by using `$(curl ifconfig.me)`

There are to ways to configure the reverse proxy file. In this script, the whole file is overwritten. This is not ideal
as some lines that are in the file may be necessary and we just want to add lines. Another way is to use the sed command, this is covered in day6 under newscript.md