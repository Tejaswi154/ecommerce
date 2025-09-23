<<<<<<< HEAD
# Use Maven + JDK image to build
FROM maven:3.9.4-eclipse-temurin-17 AS build

WORKDIR /app

# Copy Maven files
COPY pom.xml .
COPY mvnw .
COPY .mvn .mvn

# Copy source code
COPY src ./src

# Build the project
RUN mvn clean package -DskipTests

# Use JDK image for running
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /app

# Copy the built jar from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose backend port
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "app.jar"]
=======
FROM openjdk:17-jdk-alpine
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN ./mvnw clean package -DskipTests
EXPOSE 8080
CMD [\"java\", \"-jar\", \"target/backend-0.0.1-SNAPSHOT.jar\"]
>>>>>>> e2ffc23c4da067270d27904b08ff199e4075ba26
