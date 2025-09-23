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
