# Day5

User Data, file in the EC2 instance, it runs as sudo user

## Script for user data
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

```

After copy and pasting this script into user data under advanced details when creating the EC2 instance,
the code is working, however, due to the update and upgrade steps, it takes a long time to initialise.
As user data runs in the root directory, the script had to be changed to allow the code to run in the home directory.

As the code will not run in the terminal, echo statements to log the progress become redundant.

## Other pages
 - [Apache](Apache.md)
 - [Deleting AMIs](DeletingAMI.md)
 - [Speedup](Speedup.md)