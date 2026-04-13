FROM maven:3.9.14-eclipse-temurin-17-alpine
WORKDIR /app
run adduser -D appuser && chown -R appuser:appuser /app
USER appuser
COPY . .
RUN mvn package
EXPOSE 8080
CMD  ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]