# Docker vs Kubernetes

## **1. Containers Are Ephemeral**  
- Docker runs containers, but **containers are temporary** and can stop anytime.  
- If a container crashes, Docker does not restart it automatically.  

### **How Kubernetes Helps**  
- Kubernetes **monitors containers** and restarts them if they fail.  
- It ensures that the required number of containers **always stay running**.  

---

## **2. Issues Related to Scaling and Healing**  
- In Docker, you **manually create and remove** containers when demand changes.  
- If a container crashes, it must be restarted manually.  

### **How Kubernetes Helps**  
- Kubernetes **automatically scales containers** up or down based on demand.  
- If a container crashes, Kubernetes **heals** by replacing it automatically.  

---

## **3. Issues Related to Service Discovery**  
- Docker containers get **random IPs**, making it hard to connect services.  
- If a container restarts, its **IP might change**, breaking communication.  

### **How Kubernetes Helps**  
- Kubernetes assigns a **fixed DNS name** to each service.  
- Containers can communicate using **service names** instead of IPs.  

---

## **Summary**  
- **Docker runs containers**, but they are temporary and need manual management.  
- **Kubernetes automates** scaling, healing, and service discovery.  
- With Kubernetes, applications are **more reliable, scalable, and self-healing**. 🚀  
