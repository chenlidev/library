FROM ubuntu:latest as build

RUN apt-get update && \
    apt-get install -y openjdk-17-jdk maven && \
    rm -rf /var/lib/apt/lists/*

COPY . /app

WORKDIR /app

RUN mvn clean package -DskipTests

FROM openjdk:17-jdk-slim

EXPOSE 8080

COPY --from=build /app/target/library-api-0.0.1-SNAPSHOT.jar /library-api.jar

ENTRYPOINT ["java", "-jar", "/library-api.jar"]