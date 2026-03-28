# --- Stage 1: Build the Application ---
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app

# Copy the project files
COPY pom.xml .
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests

# --- Stage 2: Final Runtime Image ---
FROM tomcat:10.1-jre21-slim

LABEL "Project"="Vprofile"
LABEL "Author"="Olayinka"

# Security: Remove default webapps and sensitive info
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the war file from build stage
COPY --from=build /app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Security: Run as a non-root user
RUN groupadd -r appgroup && useradd -r -g appgroup appuser && \
    chown -R appuser:appgroup /usr/local/tomcat

USER appuser

EXPOSE 8080
WORKDIR /usr/local/tomcat
CMD ["catalina.sh", "run"]
