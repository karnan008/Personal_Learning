# Use Maven with Java 21
FROM maven:3.9.6-eclipse-temurin-21 AS build

# Set work directory
WORKDIR /app

# Copy everything into the container
COPY . .

# Compile test classes and copy dependencies
RUN mvn test-compile && \
    mvn dependency:copy-dependencies

# Use Java 21 runtime image
FROM eclipse-temurin:21

# Working directory inside container
WORKDIR /app

# Copy the built app from the previous image
COPY --from=build /app .

# Make the shell script executable
RUN chmod +x runSmoke.sh

# Run your automation script when container starts
CMD ["./runSmoke.sh"]
