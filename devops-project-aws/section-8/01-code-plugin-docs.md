# Prerequisites

### Terraform code 

Complete terraform files to create EKS in AWS VPC is available in the `eks-install` folder of this repo. This includes remote backend and statelocking implementation as well.

- `eks-install`: Folder that holds the complete terraform hcl files.
- `backend`: Folder that holds hcl files for s3 bucket and dynamodb creation.
- `modules`: Terraform Modules for VPC and EKS.
- `main.tf`: Main file that invokes the modules to create EKS in VPC.
- `variables.tf`: Variables for main.tf
- `outputs.tf`: Output values you wish to see post terraform execution, For example - `VPC ID`.

### Useful plugins to write HCL files

- `Terraform`
- `YAML`
- `GitHub Copilot`

### Documentation

- For any additional help, Terraform official documentation for AWS Provider is the best place.
