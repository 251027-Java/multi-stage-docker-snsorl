#First Stage
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src src
RUN mvn package -DskipTests


#Second Stage
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
#COPY only jar from stage 1
COPY --from=build /app/target/docker-lab-0.0.1-SNAPSHOT.jar /app/
ENTRYPOINT [ "java", "-jar", "/app/docker-lab-0.0.1-SNAPSHOT.jar" ]