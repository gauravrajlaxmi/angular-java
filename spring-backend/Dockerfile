# Build stage
FROM maven:3.9.6-eclipse-temurin-8 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Runtime stage
FROM eclipse-temurin:8-jre
WORKDIR /app
COPY --from=build /app/target/spring-backend-v1.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]


# # Use Ubuntu as base image
# FROM ubuntu:latest

# # Install dependencies
# RUN apt-get update && \
#     apt-get install -y openjdk-8-jdk maven && \
#     rm -rf /var/lib/apt/lists/*

# # Set the working directory in the container
# WORKDIR /app

# # Copy the Maven project directory into the container
# COPY . /app

# # Build the Maven project
# RUN mvn clean package -Dmaven.test.skip=true

# # Expose the port the application runs on
# EXPOSE 8080

# # Command to run the application
# CMD ["java", "-jar", "target/spring-backend-v1.jar"]
