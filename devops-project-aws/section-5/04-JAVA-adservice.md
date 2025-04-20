# Containerization of a Java based microservice

- Here are the steps that are involved in containerizing our Java based microservice. Same steps are also followed in the video.

# **Explanation of the Multi-Stage Dockerfile for a Java Microservice (Using Gradle)**  

## **Stage 1: Build Stage (Builder Image)**  
This stage is responsible for **building the Java application** using Gradle.  

1. **Use a JDK Base Image**  
   - The `eclipse-temurin:21-jdk` image is used as the build environment.  
   - This includes the necessary Java Development Kit (JDK) to compile the application.  

2. **Set the Working Directory**  
   - The working directory inside the container is set to `/usr/src/app/`.  

3. **Copy Essential Gradle Files**  
   - The `gradlew`, `settings.gradle`, and `build.gradle` files are copied to the container.  
   - The `gradle` wrapper directory is also copied to ensure Gradle can be executed inside the container.  

4. **Set Execution Permissions for Gradlew**  
   - The `chmod +x ./gradlew` command ensures the Gradle wrapper script has execution permissions.  

5. **Initialize Gradle and Download Dependencies**  
   - `./gradlew` runs the Gradle wrapper, setting up necessary configurations.  
   - `./gradlew downloadRepos` ensures that required repositories are downloaded to speed up the build.  

6. **Copy the Application Source Code**  
   - The entire project source code is copied to the container.  
   - The `pb` directory is copied into the container as `proto` (likely for protocol buffer files).  

7. **Build the Application**  
   - `./gradlew installDist -PprotoSourceDir=./proto` compiles and packages the Java application.  
   - The `-PprotoSourceDir=./proto` flag specifies the location of protocol buffer files.  

---

## **Stage 2: Runtime Stage (Final Image)**  
This stage creates a **lightweight, optimized runtime image** for running the application.  

1. **Use a Minimal JRE Base Image**  
   - The `eclipse-temurin:21-jre` image is used since it contains only the Java Runtime Environment (JRE), reducing the final image size.  

2. **Set the Working Directory**  
   - The working directory remains `/usr/src/app/`.  

3. **Copy the Built Application from the Builder Stage**  
   - The compiled application from the `builder` stage is copied into the final image.  

4. **Set Environment Variables**  
   - The `AD_PORT` environment variable is set to `9099`.  

5. **Define the Entry Point**  
   - The application is executed with `./build/install/opentelemetry-demo-ad/bin/Ad`.  
   - This is the compiled and installed binary from the Gradle `installDist` task.  

---

## **Summary**  
- The **first stage** builds the application using Gradle.  
- The **second stage** runs the built application inside a **lightweight JRE-based image**.  
- Using **multi-stage builds** ensures that the final image only contains what is necessary for execution, making it **smaller, more secure, and optimized** for production use.  
