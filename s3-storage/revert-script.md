```
#!/bin/bash

sudo sed -i 's|<img src="https://tech242-luke-first-bucket.s3.eu-west-1.amazonaws.com/scary-dog.jpg" alt="scarydog">|<img src="/images/friday13th.jpg" alt="friday13thposter">|' /repo/springapi/src/main/resources/templates/home.html

aws s3 rm s3://tech242-luke-first-bucket

cd /repo/springapi

sudo mvn package

```