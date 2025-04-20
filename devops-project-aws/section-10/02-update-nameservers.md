# Update Nameservers for Domain

## Overview
This guide will help you configure your domain purchased from GoDaddy to use AWS Route 53 for DNS management. Specifically, we will set up the domain (for example - `abhishekveeramalla.shop`) to route traffic to an AWS Application Load Balancer (ALB) using Route 53.

## Steps

### 1. Create a Hosted Zone in Route 53 [Created in the previous lecture]
1. Open the Route 53 console in the AWS Management Console.
2. Click on `Hosted zones` in the navigation pane.
3. Click on `Create hosted zone`.
4. Enter your domain name (example - `abhishekveeramalla.shop`) and select `Public Hosted Zone`.
5. Click on `Create`.

### 2. Update Nameservers in GoDaddy
1. Log in to your GoDaddy account.
2. Navigate to the `My Products` page.
3. Find your domain, example - `abhishekveeramalla.shop` and click on `DNS` or `Manage DNS`.
4. Under `Nameservers`, click on `Change`.
5. Select `Enter my own nameservers (advanced)`.
6. Enter the nameservers provided by AWS Route 53. These can be found in the Route 53 console under your hosted zone details.
7. Save the changes.

### 3. Create Record Sets in Route 53
1. In the Route 53 console, select your hosted zone for `abhishekveeramalla.shop`.
2. Click on `Create record`.
3. Create an `A` record for `www.abhishekveeramalla.shop`:
    - Name: `www`
    - Type: `A`
    - Alias: `Yes`
    - Alias Target: Select your ALB from the dropdown list.
4. Click on `Create records`.

### 4. Verify the Setup [TAKES UP TO 1-2 days as well]
1. Open a web browser and navigate to `www.abhishekveeramalla.shop`.
2. Ensure that the traffic is routed to your AWS ALB and the website loads correctly.

