# Use the Red Hat Universal Base Image 8 with Java 17
FROM registry.access.redhat.com/ubi8/ubi-minimal:latest

# Set up necessary labels
LABEL name="Data Service" \
      version="0.3.0" \
      description="Bootcamp data service application"

# Update the system, enable necessary repos
RUN microdnf install -y java-17-openjdk-headless \
 procps iputils nmap net-tools curl tar less && microdnf clean all

# Set working directory
WORKDIR /app

# Copy application into the container
COPY data-service.jar .

# Run the application
ENTRYPOINT ["java", "-jar", "data-service.jar"]
