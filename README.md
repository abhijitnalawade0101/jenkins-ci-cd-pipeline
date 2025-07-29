# jenkins-ci-cd-pipeline
Jenkins CI/CD pipeline for a Maven-based Java web application deployed on Tomcat using Docker.

This project demonstrates a complete Jenkins CI/CD pipeline for building and deploying a Java web application using:

- **Maven**: For build and dependency management
- **Tomcat**: As a servlet container
- **Docker**: For containerizing and running the application
- **Jenkins**: For automating the build and deployment process

## 🔧 How it works

1. **Source Code** is pushed to GitHub.
2. **Jenkins** pulls the code and builds the WAR file using `mvn clean package`.
3. A **Docker image** is built using `Dockerfile`, which deploys the WAR into Tomcat.
4. The image is run in a container and exposed on a custom port (e.g., 8086).

## 🐳 Dockerfile

```Dockerfile
FROM tomcat:latest
RUN cp -R /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps
COPY ./MyWebApp.war /usr/local/tomcat/webapps/
