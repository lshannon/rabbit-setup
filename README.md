# Rabbit MQ Local and PCF Set Up

This repository covers setting up Rabbit MQ both locally and in Pivotal Web Services (PWS) as a message broker for Event Driven Micro Service Architectures.

# Setting Up RabbitMQ Locally (Mac)

To build the 'simple-message-producer' locally you will need a RabbitMQ running locally, otherwise the Test will not pass as the RabbitTemplate will not be able to create a ConnectionFacactory. With a Mac installing Rabbit can be done using Brew:

```shell

brew install rabbitmq

...

brew services start rabbitmq

```
After the installation, admin console can be found here:

http://127.0.0.1:15672/

(guest/guest)

# Setting Up RabbitMQ Locally (Docker Compose)

This requires Docker Compose to be installed on your Local system:

https://docs.docker.com/compose/install/

Once Docker Composed is installed, you can get the Docker Compose file for Rabbit MQ into your local project:

```shell

curl -sSL https://raw.githubusercontent.com/bitnami/bitnami-docker-rabbitmq/master/docker-compose.yml > docker-compose.yml

```
To start the image up, run the follow command:

```shell

docker-compose up -d

```
To connect to the Rabbit MQ running in the docker image from Spring Boot, the following can be added to the application.yml file:

```yml

services:
 rabbitmq:
  image: rabbitmq:3.6.6-management
  container_name: rabbitmq
  ports:
    - "15672:15672"
    - "5672:5672"

```

# Setting Up RabbitMQ on PWS

Simply create a free instance of the CloudAMQP broker from the Marketplace:

```shell

cf create-service cloudamqp tiger scdf-rabbitmq-queue

```

Part of the Service in creating the Rabbit MQ Service is to create the manager.

![alt text](images/rabbit-manager-view.png "Rabbit Manager")

This is a useful interface to refer too. Here you can see where messages are going and what Exchanges and Queues are created.


