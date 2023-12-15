# Speeding VM up

AMI = amazon machine image.

We create an image from the instance, it will take a while to create the instance.

The image will contain the information pre-populated in the instance.

Once the image is created, we create an instance from the image, adding the cd into the correct directory and do mvn spring-boot:start