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

sudo DEBIAN_FRONTEND=noninteractive apt install -y apache2

sudo systemctl start apache2
sudo systemctl enable apache2

sudo a2enmod proxy
sudo a2enmod proxy_http

config_file="/etc/apache2/sites-available/000-default.conf"

if ! grep -q "ProxyPass / http://localhost:5000/" "$config_file"; then
    sudo sed -i '/<\/VirtualHost>/i\    ProxyPass / http:\/\/localhost:5000/' "$config_file"
fi

if ! grep -q "ProxyPassReverse / http://localhost:5000/" "$config_file"; then
    sed -i '/<\/VirtualHost>/i\    ProxyPassReverse / http:\/\/localhost:5000/' "$config_file"
fi

if ! grep -q "ProxyPreserveHost On" "$config_file"; then
    sed -i '/<\/VirtualHost>/i\    ProxyPreserveHost On' "$config_file"
fi

sudo systemctl reload apache2
```

Allows the configuration of the reverse proxy. Still doesn't work in a new AMI for some reason.