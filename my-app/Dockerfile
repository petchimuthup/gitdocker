# Use an official Maven image with OpenJDK as the base image
FROM maven

# Set the working directory inside the container
WORKDIR /my-app

# Copy the pom.xml and download dependencies (to cache them)
COPY pom.xml .

# Download Maven dependencies, useful for caching in subsequent builds
RUN mvn dependency:go-offline

# Copy the rest of the project files
COPY src ./src

# Package the application
RUN mvn clean package

# Use a minimal Java runtime for running the application
FROM openjdk
#From httpd

# Set the working directory inside the container
WORKDIR /my-app

# Copy the built jar file from the build stage
COPY --from=build /root/my-app/target/my-app-1.0-SNAPSHOT.jar ./my-app-1.0-SNAPSHOT.jar


# Expose the application port (if applicable)
EXPOSE 8080

# Define the command to run the application
CMD ["java", "-jar", "my-app-1.0-SNAPSHOT.jar"]

RUN apt update -y

