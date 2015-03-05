# Docker & spring boot = LUV!

My GOAL: create a simple flow of microservices!

Notes for the _first_ slide!

---

# Microservice?

## Microservice
- A simple well defined actor with specific capabilities
- Self contained
- Easy to spin up and down and replace


E.g. a UI can consist of multiple service.

-- hence easy to update, maintain and scale

How?

1. Using spring boot (we do not need a tomcat - we have docker!- just kill it!)
2. Deep-dive
3. ...

---

# Docker

- a Simple container based on LXC  - with a simple set of CLI!
- Docker c

# Spring Boot - From zero to hero!



- everything conventions! - I like!
- a small bootstrapped envioronment
	- a small application server / container 	
	- one jar/war to rune them all
	- get all the dependencies solve (spring/hibernate/etc... all that normally can go wrong)


[NOTE]: u update spring boot version and everything get updated and fits. a bit of a mix of what I like of JEE stuff - but you can still mix in what you like through normal spring)


# Spring Boot - small demo

## Show code!

## Run it!

```
mvn spring-boot:run
```

## Test it!

```
curl http://localhost:8080
```


simple to test. small box - simple to give to a new developer.

---

# Put the app in a docker container!

Now our java app is ready for containerzation!

# Build it!

```
cd [my project]
mvn clean install
cd target
# mac have to startup:  boot2docker start
docker build -t spring-boot-maven-docker .
```

# Run it!

// check if the image is there: docker images

```
docker run -p 8080:8080 --name demo spring-boot-maven-docker
```
now it is running its own life on a virtual environment (mine is virtual box - on linux it would be a LXC environment)


// boot2docker ip

# Test it!

curl http://<docker-IP>:8080

curl http://$(boot2docker ip):8080

## Controlling it!

docker top demo
docker ps
docker logs demo
docker stop demo
docker rm

---

# Extras

How to control an image - without rebuilding it. Interact with the spring property file.
Environment variables
-e SPRING_DATA_MONGODB_URI=mongodb://192.168.59.103/userregistration 


use it to deploy in different environments.. like dev, prod.. 

---

# Putting it together / Multiple services

Docker Compose:

```Compose is a tool for defining and running complex applications with Docker. With Compose, you define a multi-container application in a single file, then spin your application up in a single command which does everything that needs to be done to get it running.```

As said: microservices consists of many services. Docker compose, put those together in yaml:

```
web:
  build: .
  links:
   - db
  ports:
   - "8000:8000"
db:
  image: postgres
``

---

# Gotchas

Remember - tune your instance AND your host system! Even docker is nice it does not tune the OS for you!

---

# Questions
???

## Dependencies

### Docker

- docker
- docker-composer
- virtualbox (mac or m$)
- boot2docker (mac or m$)
- (git)


### Spring boot

- Java 
- maven

## Links

- http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/
