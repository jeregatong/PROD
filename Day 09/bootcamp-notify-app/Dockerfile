# Use the Red Hat Universal Base Image 8
FROM registry.access.redhat.com/ubi8/ubi-minimal:latest

# Set up necessary labels
LABEL name="NOTIFYBOD" \
      version="0.3.0" \
      description="24 by 7 Notification"

# Update the system, enable necessary repos, and install Java 8
RUN microdnf install -y java-1.8.0-openjdk-headless \
 procps iputils nmap net-tools curl tar less && microdnf clean all

# Setting Required Environment Variables
ENV JAVA_MAJOR_VERSION=8 \
 JAVA_HOME=/usr/lib/jvm/jre-1.8.0
 
# Set working directory
WORKDIR /app

# Copy application into the container
COPY fiserv-notify.jar . 

# Copy SSL cert into the container
COPY SGPVMTLRDV14.cer .
COPY SGPVMTLRDV20.cer .

# Enroll certificate
RUN keytool -import -file SGPVMTLRDV14.cer -alias SGPVMTLRDV14 -keystore /usr/lib/jvm/jre-1.8.0/lib/security/cacerts -storepass changeit -noprompt
RUN keytool -import -file SGPVMTLRDV20.cer -alias SGPVMTLRDV20 -keystore /usr/lib/jvm/jre-1.8.0/lib/security/cacerts -storepass changeit -noprompt

# Expose the port the app runs on
EXPOSE 8888

# Run the application
ENTRYPOINT ["java", "-jar", "fiserv-notify.jar"]
