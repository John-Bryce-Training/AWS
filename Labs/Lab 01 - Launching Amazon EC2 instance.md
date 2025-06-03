<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/8/89/John_bryce_logo.jpg" alt="Logo" width="259" height="107">
</p>  

| Last update | 26/03/2025  |
|-------------|-------------|

# Lab 01 - Launching Amazon EC2 instance  
Amazon EC2 (Elastic Compute Cloud) is a foundational service in AWS that allows you to run virtual machines in the cloud.   
In this lab, you will learn how to create, configure, and manage a Windows-based EC2 instance using the AWS Management Console.

## Estimated time: 50 minutes
## Overview
**Task 1:** Launching a Windows EC2 instance
  
**Task 2:** Connecting to the instance via Remote Desktop (RDP)
  
**Task 3:** Configuring Security Group rules 
 
**Task 4:** Allocating and assigning an Elastic IP 
 
**Task 5:** Monitoring the instance using Amazon CloudWatch

## Task 1: Launching a Windows EC2 instance 

#### In this task, you will launch a new Windows-based virtual machine (EC2 instance) in AWS. This is the foundation for all following tasks.  
1. Log in to the AWS Management Console - `https://eu-north-1.signin.aws.amazon.com/` using your AWS credentials.

2. From the AWS Console homepage, navigate to **EC2** by typing `EC2` in the search bar.
   
3. From the left pane click **Launch instance** to begin the process of creating a virtual machine.

![My Image](media/Lab01/01.png)
   
4. In the **Name and tags** section, enter a name for your instance: `MyWindowsInstance`.
  
5. Under **Application and OS Images (Amazon Machine Image)**, select **Windows** and than **Microsoft Windows Server 2019 Base** as the image.

6. For Instance type, select **t2.micro**. This instance type includes 1 vCPU and 1 GiB of memory.

7. Under **Key pair (login)**, click **Create new key pair**
     
| Setting                  | Value      |
|:-------------------------|:-----------|
| Name                     | `ec2lab-key` |
| Key pair type            | **RSA**        |
| Private key file format  | **.pem**       |
| Key pair type            | **RSA**        |

8. In **Network settings**, keep the default VPC and subnet.

   Make sure **Auto-assign public IP** is enabled so your instance can be reached from the internet.

9. Under **Firewall (security groups)**, click **Create security group**.

10. Under **Storage**, leave:
    - 30 GiB
    - gp2 (General Purpose SSD)
    - Delete on termination: enabled

11. Click **Launch Instance**.

## Task 2: Connect to the Windows EC2 Instance  

#### Now that your EC2 instance is running, you will connect to it using Remote Desktop Protocol (RDP), just like logging into a computer at work or school.

1. On the left menu, click **Instances**.

2. Find your instance in the list (look for the name `MyWindowsInstance`).

3. Wait until the instance state says **Running** and the status check shows **2/2 checks passed**. This means the instance is healthy and ready.

4. Select your instance by checking the box next to it.

5. Click on the **Security** tab and than choose the Security group name.

![My Image](media/Lab01/02.png)

6. At the table click on **Edit inbound rules** and than select **Add rule**.

7. At the **Type** choose **RDP** and for Source choose `My IP`. Leave all the rest as default. To finish click **"Save rules"**. 

8. Click the **Connect** button at the top.

9. In the pop-up, go to the **RDP Client** tab.

10. Click **Get Password**.

>**Note:** If the button is grayed out, wait a few more minutes — it can take up to 4 minutes after launch to be available.

11. Upload the `.pem` key file that you downloaded earlier.

12. Click **Decrypt Password**. Copy the resulting password — you will need it to log in.

13. Click **Download remote desktop file** and than choose **Connect**.

14. When prompted, enter:
    - **Username**: `Administrator`
    - **Password**: (paste the one you decrypted)
    
15. Accept the certificate warning and continue.

## Task 3: Configure Security Group Rules  

#### Security Groups are used in AWS to control which types of traffic can reach your instance. Think of them as the cloud version of a firewall.

1. From the EC2 Dashboard, click **Security Groups** on the left menu.

2. Look for the security group you created earlier and click it.

3. Go to the **Inbound rules** tab. These are the rules that define which traffic is allowed in.

4. Click **Edit inbound rules**.

5. You should see the following rule already exists:
   - **Type**: RDP
   - **Port**: 3389
   - **Source**: My IP

6. You can add additional rules if needed:
   - **HTTP**: Allows web traffic (port 80)
   - **HTTPS**: Allows secure web traffic (port 443)

7. Click **Save rules** to apply changes.

This helps control what kinds of connections can access your instance.

## Task 4: Allocate and Associate an Elastic IP  

#### Normally, if you stop and restart your EC2 instance, it will get a new public IP. To avoid this, you can assign an Elastic IP — a permanent public address.

1. On the EC2 Dashboard, scroll to the left menu and click **Elastic IPs**.

2. Click the **Allocate Elastic IP address** button.

3. Leave the default options and click **Allocate**.

4. Select the new IP address from the list.

5. Click **Associate Elastic IP address**.

6. For **Resource type**, select **Instance**.

7. In the **Instance** dropdown, select your `MyWindowsInstance`.

8. Leave the private IP field as-is and click **Associate**.

Now your instance has a public IP address that will stay the same even after reboots.

## Task 5: Monitor EC2 Performance with CloudWatch  

#### CloudWatch is a monitoring tool in AWS. It allows you to track how your instance is performing and even set alerts if something unusual happens.

1. Go back to the AWS Console home page and search for **CloudWatch**.

2. In the left menu, click **Metrics**.

3. Click **All metrics > EC2 > Per-Instance Metrics**.

4. You'll see performance metrics such as:
   - **CPUUtilization** – how much the processor is working
   - **NetworkIn/Out** – the amount of network traffic
   - **DiskRead/WriteBytes** – disk input/output activity

5. To set up an alert:
   - Click **Alarms** at the left pane and that click **In alarm**
   - Click **Create alarm**.
   - Under **Select metric** click **All metrics > EC2 > Per-Instance Metrics** and than choose a metric like **CPUUtilization**. To finish click **Select metric**. 
   - Set a condition: e.g., greater than **80** for 5 minutes
   - Click Next
   - Create a new notification by clicking at **Create new topic** and than type `MyTopic` for the **Name** and your Email address for **Email endpoints that will receive the notification**. To finish click **Create Topic**. 
   - Name your alarm (e.g., `HighCPUAlert`) and click **Create alarm**

This allows you to be notified when your instance is under heavy load.

## ✅ End of Lab  

#### 🎉 Congratulations! You’ve completed the AWS EC2 Lab.

You’ve just built and managed your first cloud-based Windows server!
