FROM gradle:8.4.0-jdk17-alpine AS builder


COPY --chown=gradle:gradle . /home/gradle/src/

WORKDIR /home/gradle/src/

# run gradle build within the container - Not the host machine
RUN gradle build -x test

FROM openjdk:17-alpine

RUN mkdir /app

COPY --from=builder /home/gradle/src/build/libs/*.jar /app/post-service.jar

ENV MONGO_DB_USERNAME=rootadmin MONGO_DB_PASSWORD=password
EXPOSE 8085
ENTRYPOINT ["java", "-jar", "app/post-service.jar"]
