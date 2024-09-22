#
# Build
#
FROM debian:10 AS build

# Install dependencies
RUN apt-get update && apt-get install -y \
    gnupg2 \
    software-properties-common \
    ca-certificates-java \
    openjdk-11-jdk-headless \
    maven \
    --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /opt/shipping

# Copy Maven configuration and resolve dependencies
COPY pom.xml /opt/shipping/
RUN mvn dependency:resolve

# Copy the source code and package the application
COPY src /opt/shipping/src/
RUN mvn package

#
# Run
#
FROM openjdk:8-jre-alpine

# Expose application port
EXPOSE 8080

# Set working directory
WORKDIR /opt/shipping

# Environment variables for service dependencies
ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

# Copy the JAR file from the build stage
COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

# Command to run the application
CMD ["java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar"]
