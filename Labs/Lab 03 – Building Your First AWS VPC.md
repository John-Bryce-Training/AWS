<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/8/89/John_bryce_logo.jpg" alt="Logo" width="259" height="107">
</p>  

| Last update | 26/03/2025  |
|-------------|-------------|

# Lab 03 - Getting Started with AWS VPC  
Amazon VPC (Virtual Private Cloud) is a foundational networking service in AWS that allows you to create isolated virtual networks in the cloud.  
It enables you to control your networking environment, including IP ranges, subnets, route tables, and gateways.  
In this lab, you will learn how to create a VPC from scratch, define public and private subnets, and configure basic routing and internet access.

### Estimated time: 60 minutes
## Overview
**Task 1:** Create a custom VPC with CIDR block 10.0.0.0/16  
 
**Task 2:** Create a public subnet and a private subnet  

**Task 3:** Create and attach an Internet Gateway  

**Task 4:** Configure route tables for public and private subnets  

**Task 5:** Launch an EC2 instance in the public subnet to test internet connectivity  

## Task 1: Create a Custom VPC

#### In this task, you will create a new Virtual Private Cloud (VPC) — a private network inside AWS — and define its IP range.

1. Log in to the AWS Management Console - `https://eu-north-1.signin.aws.amazon.com/` using your AWS credentials.

2. In the top search bar, type `VPC` and select the **VPC** service.

3. In the left menu, click **Your VPCs**.

4. Click the **Create VPC** button.

5. Choose **VPC only** (not the wizard).

6. Set the following configuration:

   - **Name tag**: `LabVPC`
   - **IPv4 CIDR**: `10.0.0.0/16` (this defines the overall IP range)
   - Leave all other options at their default values.

7. Click **Create VPC**.

## Task 2: Create Public and Private Subnets

#### Subnets divide a VPC into smaller networks. Here, you'll create one public and one private subnet in different Availability Zones.

1. In the VPC Dashboard, go to the **Subnets** section and click **Create subnet**.

2. Choose the `LabVPC` from the drop-down menu.

3. Create two subnets with the following details:

**Public Subnet:**  
- **Subnet name**: `PublicSubnet`  
- **Availability Zone**: `No preference`  
- **IPv4 subnet CIDR block**: `10.0.1.0/24`  

**Private Subnet:**  
- **Subnet name**: `PrivateSubnet`  
- **Availability Zone**: `No preference`  
- **IPv4 subnet CIDR block**: `10.0.2.0/24`

4. Click **Create subnet** after filling in both subnets.

## Task 3: Create and Attach an Internet Gateway

#### An Internet Gateway allows resources in your VPC to access the internet.

1. In the left menu, click **Internet Gateways**.

2. Click **Create internet gateway**.

3. Under **Name tag** Enter the name `LabIGW`, then click **Create internet gateway**.

4. Click **Actions** and than **Attach to VPC**.

5. Choose `LabVPC` and click **Attach internet gateway**.

## Task 4: Configure Route Tables

#### Routing controls where network traffic goes. You'll now set up a route that allows the public subnet to reach the internet.

1. In the left menu, click **Route Tables**.

2. Find the route table automatically created with `LabVPC` (you can identify it by the VPC column).

3. Rename it to `PublicRouteTable` for clarity by clicking at the pencil icon.

4. Select it and go to the **Routes** tab.

5. Click **Edit routes > Add route**:
   - **Destination**: `0.0.0.0/0` (this represents the internet)
   - **Target**: **Internet Gateway** and for the next box choose your internet gateway you created earlier.

6. Click **Save Changes**.

7. Now go to the **Subnet associations** tab > Click **Edit subnet associations**.

8. Select only the `PublicSubnet`, then click **Save associations**.

## Task 5: Launch EC2 Instance in Public Subnet

#### To test your setup, you'll launch an EC2 instance in the public subnet and check if it can access the internet.

1. In the top search bar, type `EC2` and go to the EC2 Dashboard.

2. Click **Launch instance**.

3. Fill out the instance details:
   - **Name**: `VPC-Test-Instance`
   - **Application and OS Images (Amazon Machine Image)**: Choose **Amazon Linux 2023 AMI**
   - **Instance type**: `t2.micro`
   - **Key pair**: click **Create new key pair**
     
| Setting                  | Value      |
|:-------------------------|:-----------|
| Name                     | `vpclab-key` |
| Key pair type            | **RSA**        |
| Private key file format  | **.pem**       |

And to finish click **Create key pair**. 

   - **Network**: Choose `LabVPC`
   - **Subnet**: Choose `PublicSubnet`
   - **Auto-assign public IP**: Make sure this is **enabled**
   - **Security group name**: type `vpc-scg`.

4. Click **Launch instance**.

5. After the instance is running, click on the EC2 new instance and select **connect**.

---

## ✅ End of Lab

#### 🎉 Congratulations! You’ve successfully created your first custom VPC with subnets, internet access, and a working EC2 instance.

You now understand the fundamentals of AWS networking — how to isolate resources, connect them securely, and route traffic appropriately. Great work!
