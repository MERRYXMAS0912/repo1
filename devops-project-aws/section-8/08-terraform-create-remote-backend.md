# Code explanation for S3 bucket and DynamoDB terraform file

## **1. AWS Provider Configuration**
```hcl
provider "aws" {
  region = "us-west-2"
}
```
- This block defines the **AWS provider** that Terraform will use.
- The `region` attribute specifies the AWS region where resources will be created (in this case, `us-west-2`).

---

## **2. Creating an S3 Bucket for Terraform State Storage**
```hcl
resource "aws_s3_bucket" "terraform_state" {
  bucket = "demo-terraform-eks-state-bucket"

  lifecycle {
    prevent_destroy = false
  }
}
```
- This block creates an **S3 bucket** named `demo-terraform-eks-state-bucket`.
- The `lifecycle` rule with `prevent_destroy = false` allows Terraform to delete the bucket when required.

---

## **3. Enabling Versioning for the S3 Bucket**
```hcl
resource "aws_s3_bucket_versioning" "terraform_state" {
  bucket = aws_s3_bucket.terraform_state.id
  versioning_configuration {
    status = "Enabled"
  }
}
```
- This block enables **versioning** on the S3 bucket to retain previous versions of the Terraform statefile.
- Helps with rollback and recovery in case of accidental changes.

---

## **4. Enabling Server-Side Encryption for the S3 Bucket**
```hcl
resource "aws_s3_bucket_server_side_encryption_configuration" "terraform_state" {
  bucket = aws_s3_bucket.terraform_state.id

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}
```
- This block **enables encryption** using the `AES256` algorithm to protect statefile data at rest.
- Ensures that Terraform statefiles are stored securely in the S3 bucket.

---

## **5. Creating a DynamoDB Table for State Locking**
```hcl
resource "aws_dynamodb_table" "terraform_locks" {
  name         = "terraform-eks-state-locks"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```
- This block creates a **DynamoDB table** named `terraform-eks-state-locks`.
- The table is used for **state locking**, preventing concurrent modifications to the statefile.
- `billing_mode = "PAY_PER_REQUEST"` ensures cost-effective pricing based on actual usage.
- The primary key (`hash_key`) is `LockID`, ensuring unique entries for locks.
