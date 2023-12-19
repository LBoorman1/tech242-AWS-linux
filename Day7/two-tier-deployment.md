# Two tier deployment

API & Database.

Two VMs one for the API and one for the MySQL database.

Connect between the two VMs

Database will need an extra port open to allow mysql traffic.

## Needs
 - Endpoint
 - username: root
 - password: root
Need to be specified so that the API knows these things and can access MySQL
They should be environment variables.
use the export command to set environment variables.

On the same virtual private cloud, the private IP address should be used.

