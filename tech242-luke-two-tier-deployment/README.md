# Two tier deployment

This project saw us deploy a two tier application. This included the data tier with a MySQL database and the logic tier with a Java API created by another group. This task was challenging as we had no pre-existing experience with this code base and therefore had some challenges arise when dealing with the set up.

## Instances

### App instance
The App code instance should be a t2.small instance type as the micro size does not have enough memory to
handle querying the database and hosting the application. The security group is the same, allowing, ssh from my IP
address and allow HTTP requests on the port 5000. The app code instance essentially just runs the program and sets environment variables that allow the connection to the Database instance using the correct IP address and MySQL username and password.

[Script for App Code VM](AppVMScript.md)

### Database instance
The Database instance should be a t2.micro instance with a security group that also allows the SSH from my IP address and also
opens the port 3306, which is the default MySQL port. This instance hosts the database and opens it up for connection on port 3306 from any ip address. This is achieved by configuring the MySQL password initially, then creating a new root user with the '%' wildcard as the host, which allows any IP address to connect to this root user.

[Script for Database VM](DatabaseVMScript.md)

## Blockers

One blocker experienced in this project was launching the instance using the user data. The code for the reverse proxy would not work. When visiting the IP address for the app instance, a default apache website would appear. This was overcome by changing the order of the script and configuring the reverse proxy before running the app.

