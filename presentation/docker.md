# Docker & spring boot == LUV!

My GOAL today: 

* create a simple flow of micro services!
* use it in continuous integrations

---

# Microservice?

## Microservice
- A simple well defined actor with specific capabilities
- Self contained (its own process)
- Easy to spin up and down and replace


E.g. a UI can consist of multiple service.

-- hence easy to update, maintain and scale

---

# Microservice - Martin Fowler

***
In short, the microservice architectural style [1] is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API. These services are built around business capabilities and independently deployable by fully automated deployment machinery. There is a bare minimum of centralized management of these services, which may be written in different programming languages and use different data storage technologies.
***

--- 

## How?

1. Using spring boot as application server
2. Using docker as deployment container
3. Using docker composer to orchestrate all containers into a whole application

---

# Docker

- a Simple container based on LXC  - with a simple set of CLI!
- Docker container monolith

---

# Spring Boot - From zero to hero!

- instant hero! (CRUD - paging, securing add-ons)
- everything is conventions! - I like!
- a ready bootstrapped envioronment
	- a small application server / container (embedded tomcat)
- very small footprint (fast startup!)
- one jar/war to rune them all
	- get all the dependencies solved (spring/hibernate/etc... all that normally can go wrong)

???

* we do not need explict tomcat - we have docker!- just kill it!

* you update spring boot version and everything get updated and fits. 

* what I like of JEE stuff - but you can still mix in what you like through normal spring

???

---

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
mac have to startup:  boot2docker start
docker build -t spring-boot-maven-docker .
```

# Run it!

// check if the image is there: docker images

```
docker run -p 8080:8080 --name demo spring-boot-maven-docker
```

---

# Test it!

* boot2docker ip
* curl http://<docker-IP>:8080
* curl http://$(boot2docker ip):8080

???
now it is running its own life on a virtual environment (mine is virtual box - on linux it would be a LXC environment)
???

---

# Controlling it!

* docker top demo
* docker ps
* docker logs demo
* docker stop demo
* docker rm
* CPU (cores)
* Memory 


---

# Extras

How to control an image - without rebuilding it?

* Interact with the spring property file (environment variables)
* docker run -e SPRING_DATA_MONGODB_URI=mongodb://192.168.59.103/userregistration 

use it to deploy in different environments.. like dev, prod.. 

---

# Putting it together / Multiple services

Docker Compose:

***Compose is a tool for defining and running complex applications with Docker. With Compose, you define a multi-container application in a single file, then spin your application up in a single command which does everything that needs to be done to get it running.***


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
```

---

# Gotchas
* mac - using boot2docker ip not localhost
* Remember - tune your instance AND your host system! Even docker is nice it does not tune the OS for you!
* spring boot - also tune the tommcat for threads etc.

---

# Questions
???

---

## Links

- http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/
- my github repo!


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

