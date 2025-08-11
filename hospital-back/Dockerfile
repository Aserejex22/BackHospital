FROM maven:3.9.8-eclipse-temurin-24 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn -q -e -DskipTests dependency:go-offline
COPY src ./src
RUN mvn -q -DskipTests package

FROM eclipse-temurin:24-jre
WORKDIR /app

ENV PORT=8080
ENV JAVA_OPTS="-XX:+UseContainerSupport -Xms256m -Xmx512m"

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

CMD ["sh", "-c", "java -Dserver.port=${PORT} ${JAVA_OPTS} -jar app.jar"]
