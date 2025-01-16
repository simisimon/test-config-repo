# Stage 1: Build the application
FROM maven:3.8.6-eclipse-temurin-17 AS build
WORKDIR /app

# Copy the pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy the source code and build the application
COPY src ./src
RUN mvn package -DskipTests

# Stage 2: Run the application
FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build /app/target/spring-boot-app-0.0.1-SNAPSHOT.jar app.jar

# Expose the application port
EXPOSE 8000

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
