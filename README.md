Spring Boot with Docker: Dockerizing a Spring Boot application

1. Downloading the application to Dockerize
We will dockerize a simple rest service application built with spring boot. 
You can clone the application from github 
https://github.com/srikanthrachala/spring-web/tree/master/springboot-restapi

2. Create a Dockerfile
```sh
$ cd springboot-restapi
$ vi Dockerfile
```
Update the Dockerfile with below contents

```sh

# Start with a base image containing Java runtime
FROM openjdk:8-jdk-alpine

# Add a volume pointing to /tmp
VOLUME /tmp

# Make port 8080 available to the world outside this container
EXPOSE 8080

# The application's jar file
ARG JAR_FILE=target/springboot-restapi-0.0.1-SNAPSHOT.jar

# Add the application's jar to the container
ADD ${JAR_FILE} app.jar

# Run the jar file 
ENTRYPOINT ["java","-jar","/app.jar"]

```
3. Building the Docker image
```sh
$ docker build -t srikanthrachala/springboot-restapi .
```
4. Running the docker image
```sh
$ docker run -p 5000:8080 srikanthrachala/springboot-restapi
```
or
```sh
$ docker run -d -p 5000:8080 srikanthrachala/springboot-restapi
```
5. Pushing the docker image to docker hub
```sh
$ docker login

$ docker tag srikanthrachala/springboot-restapi srikanthrachala/springboot-restapi:0.0.1-SNAPSHOT

$ docker push srikanthrachala/springboot-restapi:0.0.1-SNAPSHOT
```
It will be pushed to docker hub
https://hub.docker.com/r/srikanthrachala/springboot-restapi

6. Pulling the image from docker hub and running it
```sh
$ docker run -p 5000:8080 srikanthrachala/springboot-restapi:0.0.1-SNAPSHOT
```
