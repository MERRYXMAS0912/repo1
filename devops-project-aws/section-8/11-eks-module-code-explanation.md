# Code explanation for EKS module

## **1. Creating IAM Role for EKS Cluster**
```hcl
resource "aws_iam_role" "cluster" {
  name = "${var.cluster_name}-cluster-role"

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Action = "sts:AssumeRole"
      Effect = "Allow"
      Principal = {
        Service = "eks.amazonaws.com"
      }
    }]
  })
}
```
- Creates an **IAM role** for the EKS cluster.
- Allows **Amazon EKS** to assume this role for managing cluster operations.

---

## **2. Attaching IAM Policy to Cluster Role**
```hcl
resource "aws_iam_role_policy_attachment" "cluster_policy" {
  policy_arn = "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
  role       = aws_iam_role.cluster.name
}
```
- Attaches **AmazonEKSClusterPolicy** to the EKS cluster role.
- Grants necessary permissions for EKS to manage the cluster.

---

## **3. Creating the EKS Cluster**
```hcl
resource "aws_eks_cluster" "main" {
  name     = var.cluster_name
  version  = var.cluster_version
  role_arn = aws_iam_role.cluster.arn

  vpc_config {
    subnet_ids = var.subnet_ids
  }

  depends_on = [
    aws_iam_role_policy_attachment.cluster_policy
  ]
}
```
- Creates an **EKS cluster** with the specified name and version.
- Uses the IAM role created earlier for authorization.
- Associates the cluster with **VPC subnets** for networking.
- **Depends on** the IAM policy attachment to ensure permissions are set.

---

## **4. Creating IAM Role for Node Group**
```hcl
resource "aws_iam_role" "node" {
  name = "${var.cluster_name}-node-role"

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Action = "sts:AssumeRole"
      Effect = "Allow"
      Principal = {
        Service = "ec2.amazonaws.com"
      }
    }]
  })
}
```
- Creates an **IAM role** for the EKS worker nodes.
- Allows **EC2 instances** to assume this role.

---

## **5. Attaching IAM Policies to Node Role**
```hcl
resource "aws_iam_role_policy_attachment" "node_policy" {
  for_each = toset([
    "arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy",
    "arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy",
    "arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly"
  ])

  policy_arn = each.value
  role       = aws_iam_role.node.name
}
```
- Attaches **three AWS managed policies** to the worker node role:
  1. **AmazonEKSWorkerNodePolicy** - Grants permissions to join and interact with the EKS cluster.
  2. **AmazonEKS_CNI_Policy** - Allows the container network interface to operate properly.
  3. **AmazonEC2ContainerRegistryReadOnly** - Grants access to pull container images from ECR.

---

## **6. Creating EKS Node Group**
```hcl
resource "aws_eks_node_group" "main" {
  for_each = var.node_groups

  cluster_name    = aws_eks_cluster.main.name
  node_group_name = each.key
  node_role_arn   = aws_iam_role.node.arn
  subnet_ids      = var.subnet_ids

  instance_types = each.value.instance_types
  capacity_type  = each.value.capacity_type

  scaling_config {
    desired_size = each.value.scaling_config.desired_size
    max_size     = each.value.scaling_config.max_size
    min_size     = each.value.scaling_config.min_size
  }

  depends_on = [
    aws_iam_role_policy_attachment.node_policy
  ]
}
```
- Creates an **EKS Node Group** to run worker nodes within the cluster.
- Assigns **node IAM role** for permissions.
- Uses **subnets** for network placement.
- Defines **instance types** and **capacity type** (On-Demand or Spot instances).
- Configures **auto-scaling** with `desired_size`, `min_size`, and `max_size`.
- **Depends on** the IAM policy attachment to ensure permissions are applied.
