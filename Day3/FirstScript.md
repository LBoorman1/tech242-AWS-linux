# Creating web server script

This script will retrieve, update and upgrade packages, install a web server, restart said server and enable it to launch on startup.

```
#!/bin/bash.  --allows the script to know what shell to use

# update & upgrade
sudo apt update -y
sudo apt upgrade -y

# install web server (nginx)
sudo apt install nginx -y

# restart server
sudo systemctl restart nginx

# enable nginx
sudo systemctl enable nginx

```
Add echo statements to the file to make output more readable

`echo -e "updating... \n"` - example, -e allows use of escape character.