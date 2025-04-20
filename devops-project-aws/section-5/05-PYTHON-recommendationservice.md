# Containerization of a Python based microservice

- Here are the steps that are involved in containerizing our Python based microservice. Same steps are also followed in the video.

## **Stage 1: Base Image Setup**  
This stage is responsible for **setting up the environment and installing dependencies** for the Python application.  

1. **Use a Minimal Python Base Image**  
   - The `python:3.12-slim-bookworm` image is used to keep the container lightweight.  
   - "Slim" versions of Python images contain only essential packages, reducing image size.  

2. **Set the Working Directory**  
   - The working directory inside the container is set to `/usr/src/app/`.  

3. **Copy Dependency File**  
   - The `requirements.txt` file is copied into the container to install dependencies.  

4. **Upgrade Pip**  
   - `pip install --upgrade pip` ensures that the latest version of `pip` is used.  

5. **Install Dependencies**  
   - `pip install -r requirements.txt` installs all required Python packages.  

6. **Copy the Application Source Code**  
   - The entire project source code is copied into the container.  

7. **Install OpenTelemetry Dependencies**  
   - `opentelemetry-bootstrap -a install` installs OpenTelemetry auto-instrumentation for tracing and monitoring.  

8. **Set Environment Variables**  
   - `RECOMMENDATION_PORT` is set to `1010`, defining the port the service will use.  

9. **Define the Entry Point**  
   - The application is executed with `python recommendation_server.py`.  
   - This runs the Python microservice when the container starts.  

---

## **Summary**  
- The **Dockerfile** sets up a **lightweight Python environment** with all necessary dependencies.  
- The **OpenTelemetry auto-instrumentation** is installed for monitoring.  
- The final image runs the **Python microservice efficiently** with minimal overhead.   
