```
sudo wget https://i.pinimg.com/736x/bd/4a/f4/bd4af4a50534b17aa70b732a592b3933.jpg

sudo mv bd4af4a50534b17aa70b732a592b3933.jpg scary-dog.jpg

aws s3 cp scary-dog.jpg s3://tech242-luke-first-bucket

aws s3api put-object-acl --bucket tech242-luke-first-bucket --key scary-dog.jpg --acl public-read

sudo sed -i 's|<img src="/images/friday13th.jpg" alt="friday13thposter">|<img src="https://tech242-luke-first-bucket.s3.eu-west-1.amazonaws.com/scary-dog.jpg" alt="scarydog">|' /repo/springapi/src/main/resources/templates/home.html

sudo mvn package
```
