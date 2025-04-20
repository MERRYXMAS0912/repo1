# Terraform Statefile: The Brain of Terraform

## **What is a Terraform Statefile?**
- Terraform maintains a statefile (`terraform.tfstate`) that records information about managed infrastructure.
- It acts as the single source of truth for Terraform and helps track resource mappings between Terraform configurations and real-world infrastructure.

## **Why is the Statefile Important?**
- **Tracking Resources:** Terraform uses the statefile to understand which resources it manages.
- **Performance Optimization:** Instead of querying cloud providers every time, Terraform reads from the statefile to improve performance.
- **Dependency Management:** It helps Terraform determine resource dependencies and execution order.
