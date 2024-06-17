# Build stage
FROM openjdk:11 AS BUILD_IMAGE

# Install Maven
RUN apt-get update && apt-get install -y maven git

# Clone the repository and build the project
RUN git config --global http.postBuffer 524288000
RUN git clone https://github.com/dey-yemi/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

# Application stage
FROM tomcat:9-jre11

LABEL "Project"="Vprofile"
LABEL "Author"="Deyemijoshua"

# Clean the webapps directory
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the built WAR file from the build stage
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose port 8080
EXPOSE 8080

# Run Tomcat
CMD ["catalina.sh", "run"]
