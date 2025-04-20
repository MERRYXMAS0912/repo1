# Route 53 Hosted Zone

## What is Route 53 Hosted Zone?

Amazon Route 53 is a scalable and highly available Domain Name System (DNS) web service. A hosted zone is a container for records, which include information about how you want to route traffic for a specific domain (such as example.com) and its subdomains.

### Types of Hosted Zones

1. **Public Hosted Zone**: Used to manage the DNS records for a domain that is accessible from the internet.
2. **Private Hosted Zone**: Used to manage the DNS records for a domain that is accessible only from within one or more Amazon VPCs.

### Steps to Create a Hosted Zone

1. **Sign in to the AWS Management Console**:
    - Open the [Route 53 console](https://console.aws.amazon.com/route53/).

2. **Create a Hosted Zone**:
    - In the navigation pane, choose **Hosted zones**.
    - Choose **Create hosted zone**.
    - In the **Create Hosted Zone** pane, enter the following values:
      - **Domain Name**: Enter the name of the domain that you want to route traffic for.
      - **Type**: Choose either **Public Hosted Zone** or **Private Hosted Zone**.
      - **VPC ID**: If you chose **Private Hosted Zone**, select the VPC that you want to associate with the hosted zone.
    - Choose **Create**.

