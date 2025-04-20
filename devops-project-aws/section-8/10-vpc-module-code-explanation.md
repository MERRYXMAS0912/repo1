# Code explanation for VPC module

## **1. Creating a VPC**
```hcl
resource "aws_vpc" "main" {
  cidr_block           = var.vpc_cidr
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Name                                           = "${var.cluster_name}-vpc"
    "kubernetes.io/cluster/${var.cluster_name}"    = "shared"
  }
}
```
- Creates a **VPC (Virtual Private Cloud)** using the CIDR block specified in `var.vpc_cidr`.
- Enables **DNS support** and **DNS hostnames** for instances in the VPC.
- Adds tags for Kubernetes cluster integration and identification.

---

## **2. Creating Private Subnets**
```hcl
resource "aws_subnet" "private" {
  count             = length(var.private_subnet_cidrs)
  vpc_id            = aws_vpc.main.id
  cidr_block        = var.private_subnet_cidrs[count.index]
  availability_zone = var.availability_zones[count.index]

  tags = {
    Name                                           = "${var.cluster_name}-private-${count.index + 1}"
    "kubernetes.io/cluster/${var.cluster_name}"    = "shared"
    "kubernetes.io/role/internal-elb"              = "1"
  }
}
```
- Creates multiple **private subnets** based on `private_subnet_cidrs`.
- Each subnet is assigned an **availability zone** from `availability_zones`.
- Tags define Kubernetes cluster association and **internal load balancer** role.

---

## **3. Creating Public Subnets**
```hcl
resource "aws_subnet" "public" {
  count             = length(var.public_subnet_cidrs)
  vpc_id            = aws_vpc.main.id
  cidr_block        = var.public_subnet_cidrs[count.index]
  availability_zone = var.availability_zones[count.index]

  map_public_ip_on_launch = true

  tags = {
    Name                                           = "${var.cluster_name}-public-${count.index + 1}"
    "kubernetes.io/cluster/${var.cluster_name}"    = "shared"
    "kubernetes.io/role/elb"                       = "1"
  }
}
```
- Creates multiple **public subnets** based on `public_subnet_cidrs`.
- Assigns **public IP addresses** to instances on launch.
- Tags specify Kubernetes cluster association and **public load balancer** role.

---

## **4. Creating an Internet Gateway**
```hcl
resource "aws_internet_gateway" "main" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "${var.cluster_name}-igw"
  }
}
```
- Creates an **Internet Gateway** to enable internet access for public subnets.

---

## **5. Creating NAT Gateway and Elastic IPs**
```hcl
resource "aws_eip" "nat" {
  count = length(var.public_subnet_cidrs)
  domain = "vpc"

  tags = {
    Name = "${var.cluster_name}-nat-${count.index + 1}"
  }
}

resource "aws_nat_gateway" "main" {
  count         = length(var.public_subnet_cidrs)
  allocation_id = aws_eip.nat[count.index].id
  subnet_id     = aws_subnet.public[count.index].id

  tags = {
    Name = "${var.cluster_name}-nat-${count.index + 1}"
  }
}
```
- **Elastic IPs (EIPs)** are created for the **NAT gateways**.
- **NAT gateways** allow private subnet instances to access the internet securely.
- Each NAT gateway is associated with a **public subnet**.

---

## **6. Creating Route Tables**
```hcl
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.main.id
  }

  tags = {
    Name = "${var.cluster_name}-public"
  }
}
```
- **Public route table** routes internet traffic (`0.0.0.0/0`) to the Internet Gateway.

```hcl
resource "aws_route_table" "private" {
  count  = length(var.private_subnet_cidrs)
  vpc_id = aws_vpc.main.id

  route {
    cidr_block     = "0.0.0.0/0"
    nat_gateway_id = aws_nat_gateway.main[count.index].id
  }

  tags = {
    Name = "${var.cluster_name}-private-${count.index + 1}"
  }
}
```
- **Private route tables** route internet traffic through **NAT gateways**.

---

## **7. Associating Route Tables with Subnets**
```hcl
resource "aws_route_table_association" "private" {
  count          = length(var.private_subnet_cidrs)
  subnet_id      = aws_subnet.private[count.index].id
  route_table_id = aws_route_table.private[count.index].id
}
```
- Associates each **private subnet** with a **private route table**.

```hcl
resource "aws_route_table_association" "public" {
  count          = length(var.public_subnet_cidrs)
  subnet_id      = aws_subnet.public[count.index].id
  route_table_id = aws_route_table.public.id
}
```
- Associates all **public subnets** with the **public route table**.