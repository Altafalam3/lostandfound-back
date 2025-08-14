# Use Eclipse Temurin JDK 21 as base image
FROM eclipse-temurin:21-jdk

# Set working directory inside container
WORKDIR /app

# Copy Maven wrapper and config files
COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .

# Make mvnw executable (fix for Permission denied)
RUN chmod +x mvnw

# Download dependencies (cached in Docker layer)
RUN ./mvnw dependency:go-offline -B

# Copy the source code
COPY src src

# Build the application (skip tests for faster build)
RUN ./mvnw clean package -DskipTests

# Run the application
CMD ["java", "-jar", "target/lostandfound-0.0.1-SNAPSHOT.jar"]
