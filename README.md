# Spring boot User Beans

[![CI Builds](https://github.com/jabrena/spring-boot-user-beans/actions/workflows/build.yaml/badge.svg?branch=main)](https://github.com/jabrena/spring-boot-user-beans/actions/workflows/build.yaml)

[![SonarCloud](https://sonarcloud.io/images/project_badges/sonarcloud-white.svg)](https://sonarcloud.io/summary/new_code?id=jabrena_spring-boot-user-beans)

A visual way to increase the developer awareness to minimize the number of Beans that they maintain in memory.

![](./docs/user-beans2.png)

## Requirements

- [x] Visualize Beans running in the container
- [x] List of user dependencies (Jars)
- [x] List of user dependencies (Jars) & packages
- [x] List of user beans
- [x] List of dependencies (Jars) & Beans
- [ ] Review quality of results
- [ ] Learn to disable beans not used

## Convention over configuration

Convention over configuration (also known as coding by convention) is a software design paradigm used by software frameworks that attempts to decrease the number of decisions that a developer using the framework is required to make without necessarily losing flexibility and don't repeat yourself (DRY) principles.

https://en.wikipedia.org/wiki/Convention_over_configuration

## How to run in local

```bash
mvn clean verify
mvn spring-boot:run -pl examples/hello-world/ -am -Puserbeans
mvn clean test -Dtest=UserDependenciesServiceTests#getDependencyDocuments -pl spring-boot-user-beans-starter/
mvn clean test -Dtest=UserBeansServiceTests#shouldReturnsAllBeansInformation -pl spring-boot-user-beans-starter/

#UX
curl -v http://localhost:8080/actuator/userbeans/graph2-combo | json_pp
curl -v http://localhost:8080/actuator/userbeans/graph2 | json_pp

curl -v http://localhost:8080/actuator/userbeans/dependencies | json_pp
curl -v http://localhost:8080/actuator/userbeans/dependencies/packages | json_pp
curl -v http://localhost:8080/actuator/userbeans/dependencies/beans | json_pp
curl -v http://localhost:8080/actuator/userbeans/beans | json_pp
```

## Configuration

Enabling this spring boot property to enable this feature:

```
management.endpoints.web.exposure.include=beans,userbeans
```

## Spring Boot CLI

```
sdk install springboot
spring init -d=web,devtools --build=maven --force ./
```

## How to show the coverage on Codespaces?

```bash
# Step 1: Launch the webserver with the JACOCO Report
mvn clean verify
sdk install java 20-tem
sdk use java 20-tem
jwebserver -p 9000 -d "$(pwd)/coverage-module/target/site/jacoco-aggregate/"

# Step 2: Stop the webserver & use the default Java version
sdk env install
sdk env
```

## Other commands

```
./mvnw prettier:write
./mvnw versions:display-dependency-updates
./mvnw versions:display-plugin-updates
```

## References

- https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/package-summary.html
- https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/package-summary.html
- https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/
- https://www.jetbrains.com/help/idea/spring-diagrams.html#spring-beans-diagram
- https://github.com/making/beansviz-spring-boot-actuator
- https://docs.spring.io/spring-boot/docs/current/reference/html/cli.html#cli.using-the-cli
- https://github.com/j3soon/directed-graph-visualization
- https://d3js.org/
- https://www.webjars.org/all
- https://www.eclemma.org/jacoco/trunk/doc/maven.html
