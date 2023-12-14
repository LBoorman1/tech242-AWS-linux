# Deployment

## Three tier deployment

- Application tier - frontend
- Logic tier - backend API
- Data tier - database

## SCP files to remote

`scp -i ".ssh/tech242.pem" text.txt ubuntu@ip:~` - copy a file called text.txt to remote
`scp -i ".ssh/tech242.pem" -r test ubuntu@ip:~` - copy directory called test to remote.

## Linux commands

adding `sudo DEBIAN_FRONTEND=noninteractive` to a command gets rid of the need for user input in the command.

## Deployment today

As the application uses a mongo atlas database, we have a two tier deployment essentially. It deploys the application which contains
the frontend and backend code.

We used a pre-existing Sparta project called the json-voorhees-app.