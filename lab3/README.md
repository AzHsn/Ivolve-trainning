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
FROM maven:3.9.14-eclipse-temurin-17-alpine
WORKDIR /app
run adduser -D appuser && chown -R appuser:appuser /app
USER appuser
COPY . .
RUN mvn package
EXPOSE 8080
CMD  ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]
```````
#### 3. Build the Docker Image

````bash
docker build -t app1 .
docker run -d -p 8080:8080 --name container1 mav:v1.0

``````

5. Test the Application
````
curl http://localhost:8080
````
Or open your browser at http://localhost:8080.

![browser](./Screenshot%202026-04-13%20225845.png)

To view container logs:

````
docker logs container1

abdelazez@LAPTOP-MMJEGKRB:~/Ivolve-trainning/lab3/Docker-1$ docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED         STATUS         PORTS                                       NAMES
58022ec90bdd   mav:v1.0   "/usr/local/bin/mvn-…"   4 seconds ago   Up 3 seconds   0.0.0.0:4532->8080/tcp, :::4532->8080/tcp   nice_cray
abdelazez@LAPTOP-MMJEGKRB:~/Ivolve-trainning/lab3/Docker-1$ cd ..
abdelazez@LAPTOP-MMJEGKRB:~/Ivolve-trainning/lab3$ ls
Docker-1
abdelazez@LAPTOP-MMJEGKRB:~/Ivolve-trainning/lab3$ git remote 
origin
abdelazez@LAPTOP-MMJEGKRB:~/Ivolve-trainning/lab3$ docker logs nice_cray 
mkdir: cannot create directory ‘/root’: Permission denied
Can not write to /root/.m2/copy_reference_file.log. Wrong volume permissions? Carrying on ...       

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v3.2.0)

2026-04-13T20:57:11.583Z  INFO 1 --- [           main] com.example.demo.DemoApplication         : Starting DemoApplication v0.0.1-SNAPSHOT using Java 17.0.18 with PID 1 (/app/target/demo-0.0.1-SNAPSHOT.jar started by appuser in /app)
2026-04-13T20:57:11.594Z  INFO 1 --- [           main] com.example.demo.DemoApplication         : No active profile set, falling back to 1 default profile: "default"
2026-04-13T20:57:13.216Z  INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port 8080 (http)
2026-04-13T20:57:13.239Z  INFO 1 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2026-04-13T20:57:13.240Z  INFO 1 --- [           main] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/10.1.16]
2026-04-13T20:57:13.305Z  INFO 1 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2026-04-13T20:57:13.307Z  INFO 1 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 1549 ms
2026-04-13T20:57:13.882Z  INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port 8080 (http) with context path ''
2026-04-13T20:57:13.901Z  INFO 1 --- [           main] com.example.demo.DemoApplication         : Started DemoApplication in 3.037 seconds (process running for 3.725)
2026-04-13T20:58:33.119Z  INFO 1 --- [nio-8080-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2026-04-13T20:58:33.120Z  INFO 1 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2026-04-13T20:58:33.124Z  INFO 1 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 4 ms
````
1. Stop and Delete the Container
````
docker stop container1
docker rm container1
````
Optional – remove the image:

````
docker rmi mav:v1.0
````