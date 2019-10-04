Password API
============

[![Build Status](https://travis-ci.org/nicopaez/passwordapi-java.svg?branch=master)](https://travis-ci.org/nicopaez/passwordapi-java)

This project is based on Java 8 and Maven 3.

* Build: mvn clean compile
* Test: mvn clean test
* Run the app: mvn clean spring-boot:run
* Package: mvn clean package

docker build -t nicopaez/passwordapi-java:$VERSION . --build-arg JAR_FILE=./target/passwordapi-$VERSION.jar

docker build -t nicopaez/passwordapi-java:$VERSION-fabric8.openjdk8 . --build-arg JAR_FILE=./target/passwordapi-$VERSION.jar

hola
