#
# Build stage
#
FROM maven:3.6.0-jdk-11-slim AS build
COPY ./server/src /home/app/src
COPY ./server/pom.xml /home/app
RUN mvn -f /home/app/pom.xml clean compile assembly:single

#
# Package stage
#
FROM openjdk:11-jre-slim
COPY --from=build /home/app/target/minecraft-server-rest-1.0.0.jar /usr/local/lib/serverController.jar
COPY ./server.jar /root/server.jar
COPY ./eula.txt /root/eula.txt
EXPOSE 8080
EXPOSE 25565
ENTRYPOINT ["java","-jar","/usr/local/lib/serverController.jar"]