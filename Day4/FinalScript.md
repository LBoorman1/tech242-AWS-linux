# Final Script

The code will update and upgrade relevant packages, install maven, java and git, clone the relevant repo and run the application.

```
#!/bin/bash

#update and upgrade
sudo DEBIAN_FRONTEND=noninteractive apt update -y
sudo apt upgrade -y

#install maven
sudo DEBIAN_FRONTEND=noninteractive apt install -y maven
mvn -version

#install jdk (java) 17
sudo DEBIAN_FRONTEND=noninteractive apt install -y openjdk-17-jdk
java -version

#install git
sudo DEBIAN_FRONTEND=noninteractive apt install git

#delete repo from remote if exists
cd ~/app-code
rm -rf tech242-jsonvoorhees-app

#copy the app code to the VM
git clone https://github.com/LBoorman1/tech242-jsonvoorhees-app.git

#cd to proper directory
cd ~/app-code/tech242-jsonvoorhees-app/springapi

#start the application
mvn spring-boot:start
```