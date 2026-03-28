# --- Stage 1: Build the Application ---
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app

# Copy the project files (Maven needs these to build!)
COPY pom.xml .
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests

# --- Stage 2: Final Runtime Image ---
FROM tomcat:10.1-jre21

LABEL "Project"="Vprofile"
LABEL "Author"="Olayinka"

RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the war file from build stage
COPY --from=build /app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
WORKDIR /usr/local/tomcat
CMD ["catalina.sh", "run"]
