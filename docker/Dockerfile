# GET a base image with java7
FROM dockerfile/java:oracle-java7

MAINTAINER slarsen@braintrust.dk

# add our local jar to the file system
ADD spring-boot-maven-docker.jar /opt/spring-boot-maven-docker/

# expose port 8080 (default spring boot port)
EXPOSE 8080

# set our working directory
WORKDIR /opt/spring-boot-maven-docker/

# bootup our spring application by running a normal java -jar *.jar file
CMD ["java", "-jar", "spring-boot-maven-docker.jar"]