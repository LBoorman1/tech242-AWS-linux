# App VM Script

sudo DEBIAN_FRONTEND=noninteractive apt update -y
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y

sudo DEBIAN_FRONTEND=noninteractive apt install mysql-client -y
sudo DEBIAN_FRONTEND=noninteractive apt install maven -y
sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y

sudo DEBIAN_FRONTEND=noninteractive apt install git -y

cd ~
rm -rf repo

git clone https://github.com/LBoorman1/tech242-luke-world-repository.git ~/repo

cd repo/WorldProject

export DB_HOST=jdbc:mysql://172.31.61.145:3306/world
export DB_USER=root
export DB_PASS=root

output=$(mysql -h 172.31.54.27 -u root -proot -e "USE world; SELECT 1" 2>&1)

if [ $? -eq 0 ]; then
    echo "Connected Successfully"
    mvn clean package spring-boot:start
else
    echo "Failed to connect"
    echo $output
fi

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

