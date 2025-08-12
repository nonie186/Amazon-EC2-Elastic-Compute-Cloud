# Task 1: Launching your EC2 instance
  In this task, you will launch an Amazon EC2 instance with termination protection. 
  Termination protection prevents you from accidentally terminating an EC2 instance. 
  You will deploy your instance with a User Data script that will allow you to deploy a simple web server.

In the AWS Management Console on the Services menu, choose EC2.

<img width="1337" height="449" alt="console" src="https://github.com/user-attachments/assets/5d760cb8-a46d-4f6a-875b-dbe26444ae2d" />


In the left navigation pane, choose EC2 Dashboard to ensure that you are on the dashboard page.

Choose Launch instance, and then select Launch instance.

## Step 1: Naming your EC2 instance
When you name your instance, AWS creates a key value pair. The key for this pair is Name, and the value is the name you enter for your EC2 instance.

In the Name and tags pane, in the Name text box, enter Web Server.

## Step 2: Choosing an Amazon Machine Image (AMI)
An AMI provides the information required to launch an instance, which is a virtual server in the cloud. An AMI includes the following:

A template for the root volume for the instance (for example, an operating system or an application server with applications)

Launch permissions that control which AWS accounts can use the AMI to launch instances

A block device mapping that specifies the volumes to attach to the instance when it is launched

The Quick Start list contains the most commonly used AMIs. You can also create your own AMI or select an AMI from the AWS Marketplace, an online store where you can sell or buy software that runs on AWS.

Locate the Application and OS Images (Amazon Machine Image) pane. 

Under AMI Machine Image (AMI), notice that the Amazon Linux 2023* image is selected by default. Keep this setting.

## Step 3: Choosing an instance type
Amazon EC2 provides a wide selection of instance types optimized to fit different use cases. Instance types comprise varying combinations of CPU, memory, storage, and networking capacity and give you the flexibility to choose the appropriate mix of resources for your applications. Each instance type includes one or more instance sizes so that you can scale your resources to the requirements of your target workload.

Select a t3.micro instance. This instance type has 2 virtual CPU and 1 GiB of memory.

From the dropdown, select t3.micro.

NOTE: You may be restricted from using other instance types in this lab.

## Step 4: Configuring a key pair
Amazon EC2 uses public–key cryptography to encrypt and decrypt login information. To log in to your instance, you must create a key pair, specify the name of the key pair when you launch the instance, and provide the private key when you connect to the instance.

In this lab, you do not log in to your instance, so you do not require a key pair.

In the Key pair (login) pane, select Proceed without a key pair (Not recommended).

## Step 5: Configuring the network settings 
You use this pane to configure networking settings.

The VPC indicates which virtual private cloud (VPC) you want to launch the instance into. You can have multiple VPCs, including different ones for development, testing, and production.

In the Network settings pane, choose Edit

For VPC - required, select Lab VPC.

Still in the Network settings pane, configure the Security Group as follows:

Security group name - required: Web Server security group

Description: Security group for my web server

A security group acts as a virtual firewall that controls the traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance. You add rules to each security group that allow traffic to or from its associated instances. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group.

Under Inbound security groups rules select the Remove

In this lab, you will not log into your instance using SSH. Removing SSH access will improve the security of the instance.

## Step 6: Adding storage
Amazon EC2 stores data on a network-attached virtual disk called Amazon Elastic Block Store (Amazon EBS).

You launch the EC2 instance using a default 8 GiB disk volume. This is your root volume (also known as a boot volume).

In the Configure storage pane, keep the default storage configuration.

## Step 7: Configuring advanced details 
Expand the Advanced details pane.

Select the dropdown for Termination protection, then choose Enable.

When you launch an instance in Amazon EC2, you have the option of passing user data to the instance. These commands can be used to perform common automated configuration tasks and even run scripts after the instance starts. 

Copy the following commands, and paste them into the User data text box.

> #!/bin/bash
> yum -y install httpd
> systemctl enable httpd
> systemctl start httpd
> echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
> The script does the following:

Install an Apache web server (httpd)

Configure the web server to automatically start on boot

Activate the Web server

Create a simple web page

## Step 8: Launching an EC2 instance
Now that you have configured your EC2 instance settings, it is time to launch your instance.

In the right pane, choose Launch instance

Choose View all instances

The instance appears in a Pending state, which means it is being launched. It then changes to Running, which indicates that the instance has started booting. There will be a short time before you can access the instance.

The instance receives a public DNS name that you can use to contact the instance from the Internet.

Select the  box next to your Web Server. The Details tab displays detailed information about your instance.

 To view more information in the Details tab, drag the window divider upward.

Review the information displayed in the Details, Security and Networking tabs.

Wait for your instance to display the following:

Note: Refresh if needed.

Instance State:  Running

Status Checks:   2/2 checks passed

## Task 2: Monitor Your Instance
Monitoring is an important part of maintaining the reliability, availability, and performance of your Amazon Elastic Compute Cloud (Amazon EC2) instances and your AWS solutions.

Select the instance by checking the box next to the instance and navigate to the bottom of the screen to the Status checks tab.

 With instance status monitoring, you can quickly determine whether Amazon EC2 has detected any problems that might prevent your instances from running applications. Amazon EC2 performs automated checks on every running EC2 instance to identify hardware and software issues.

Notice that both the System reachability and Instance reachability checks have passed.

Select the Monitoring tab.

This tab displays Amazon CloudWatch metrics for your instance. Currently, there are not many metrics to display because the instance was recently launched.

You can choose a graph to see an expanded view.

 Amazon EC2 sends metrics to Amazon CloudWatch for your EC2 instances. Basic (five-minute) monitoring is enabled by default. You can enable detailed (one-minute) monitoring.

In the Actions  menu, select Monitor and troubleshoot  Get Instance Screenshot.

This shows you what your Amazon EC2 instance console would look like if a screen were attached to it.


# The **challenges, growth, and wins** for your EC2 project in a clear, reflective way:

## **Challenges**

* **Understanding AWS services and configurations** – Navigating the AWS Management Console for the first time required familiarizing myself with concepts like AMIs, instance types, VPCs, and security groups.
* **Balancing security with accessibility** – Removing SSH access for better security meant relying entirely on automated User Data scripts, which needed to work perfectly on first run.
* **Termination protection setup** – Ensuring that the feature was correctly enabled so the instance couldn’t be accidentally deleted added an extra layer of caution to the process.

## **Growth**

* **Hands-on experience with EC2 provisioning** – I learned how to launch, configure, and secure an Amazon EC2 instance from scratch.
* **Improved cloud security awareness** – Gained an understanding of how security groups act as virtual firewalls and how to configure them for specific use cases.
* **Automation skills** – Successfully implemented a User Data script to deploy and configure an Apache web server automatically at launch.
* **Monitoring awareness** – Learned to use the EC2 Status Checks and CloudWatch metrics to monitor performance and system health.

## **Wins**

* **Successfully launched a functional web server** – The instance displayed “Hello From Your Web Server!” exactly as intended.
* **Achieved 2/2 status checks passed** – Verified the instance was fully operational and healthy.
* **Applied best practices** – Used termination protection, avoided unnecessary open ports, and followed structured deployment steps.
* **Connected learning to real-world application** – Understood how the skills in launching and monitoring EC2 instances apply directly to production environments.
