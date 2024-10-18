FROM gradle:8.8-jdk-21-and-22 AS build

WORKDIR /app

COPY build.gradle.kts settings.gradle.kts gradlew /app/

COPY src /app/src

RUN gradle bootJar --no-daemon

FROM eclipse-temurin:21-jre AS runtime

RUN groupadd -r spring && useradd -r -g spring spring
USER spring:spring

COPY --from=build /app/build/build/libs/*.jar /app/app.jar

EXPOSE 8080

CMD ["java", "-jar", "/app/app.jar"]
