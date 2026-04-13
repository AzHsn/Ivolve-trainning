# Lab 3: Run Java Spring Boot App in a Container

## Objective
- Clone a Spring Boot application
- Write a Dockerfile to build and run the app inside a container
- Build a Docker image
- Run a container, test it, then stop and remove it

## Prerequisites
- **Docker** installed ([Get Docker](https://docs.docker.com/get-docker/))
- **Git** installed
- **Internet connection**

Verify Docker is running:
```bash
docker --version
````
Step-by-Step Instructions
1. Clone the Application Code
``````
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
````````
1. Write the Dockerfile
Create a file named Dockerfile in the Docker-1/ directory with the following content:
````
FROM maven:3.9.14-eclipse-temurin-17-alpine AS builder
WORKDIR /app
run adduser -D appuser && chown -R appuser:appuser /app
USER appuser
COPY . .

RUN mvn clean package -DskipTests

FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

COPY --from=builder /app/target/demo-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
```````
#### 3. Build the Docker Image

````bash
docker build -t m-stage .
docker run -d -p 5435:8080 --name containert m-stage

``````

5. Test the Application
````
curl http://localhost:5435
````
Or open your browser at http://localhost:5435.

![browser](./Screenshot%202026-04-13%20225845.png)

To view container logs:

````
docker logs container5


  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v3.2.0)

2026-04-13T21:45:37.720Z  INFO 1 --- [           main] com.example.demo.DemoApplication         : Starting DemoApplication v0.0.1-SNAPSHOT using Java 17.0.18 with PID 1 (/app/app.jar started by root in /app)
2026-04-13T21:45:37.729Z  INFO 1 --- [           main] com.example.demo.DemoApplication         : No active profile set, falling back to 1 default profile: "default"
2026-04-13T21:45:39.422Z  INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port 8080 (http)
2026-04-13T21:45:39.438Z  INFO 1 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2026-04-13T21:45:39.438Z  INFO 1 --- [           main] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/10.1.16]
2026-04-13T21:45:39.504Z  INFO 1 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2026-04-13T21:45:39.506Z  INFO 1 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 1586 ms
2026-04-13T21:45:40.066Z  INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port 8080 (http) with context path ''
2026-04-13T21:45:40.083Z  INFO 1 --- [           main] com.example.demo.DemoApplication         : Started DemoApplication in 3.034 seconds (process running for 3.67)
````
1. Stop and Delete the Container
````
docker stop container5
docker rm container5
````
Optional – remove the image:

````
docker rmi m-stage
````