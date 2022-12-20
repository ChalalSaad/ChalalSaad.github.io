---
title: creating a VPC and launch web application on Amazone EC2
date: 15,dec 2022 
categories : [cloud,AWS compute services]
tags: [cloud,Amazon EC2,Security,Networking,virtual machine,VPC,deployment]
---

# Cloud ?
![cloud pic](/assets/cloud.jpg)
The cloud is a datacenter  , that's all , if you have a company you should create a space to install your  own servers , so you will need high capacity of electricity ,when you have a hundred of servers in your datacenter and every one consume 200 W or 500 W  that's mean a lot of  KW of heat in closed zone , you need air conditioner .   People to maintain the servers , security (hardware , software).
The cloud help you to ovoid all these problems , you will spend more time to scale your application **Time to market**.<br>
this is my  own definition you can know more from [Google](https://letmegooglethat.com/?q=cloud).<br>
So anyone can make his  own servers and start to deploying , cloning , managing ... , in the past only the monsters  companies who can attack world clients, but today nobody live on  the end of this planet can buy a server on Tokyo or London ...
### Top 10 Cloud Service Providers Globally in 2022:
1. Amazon Web Services (AWS)
2. Microsoft Azure
3. Google Cloud Platform (GCP)
4. Alibaba Cloud
5. Oracle Cloud
6. IBM Cloud (Kyndryl)
7. Tencent Cloud
8. OVHcloud
9. DigitalOcean
 10. Linode (Akamai)

## AWS :
![aws-pic](/assets/aws.png)

Well AWS simply just provides cloud computing services. Those IT resources mentioned in the cloud computing definition are AWS services in this case. We’ll need to use these AWS services to architect a scalable, highly available, and cost effective infrastructure to host our corporate directory application. This way we can get our corporate directory app out into the world quickly, without having to manage any heavy-duty physical hardware. There are the six main advantages to running your workloads on AWS.

## The Six Benefits of Cloud Computing

***Pay as you go. Instead of investing in data centers and hardware before you know how you are going to use them, you pay only when you use computing resources, and pay only for how much you use.***

***Benefit from massive economies of scale. By using cloud computing, you can achieve a lower cost than you can get on your own. Because usage from hundreds of thousands of customers is aggregated in the cloud, AWS can achieve higher economies of scale, which translates into lower pay as-you-go prices.***
 
***Stop guessing capacity. Eliminate guessing on your infrastructure capacity needs. When you make a capacity decision prior to deploying an application, you often end up either sitting on expensive idle resources or dealing with limited capacity. With cloud computing, these problems go away. You can access as much or as little capacity as you need, and scale up and down as required with only a few minutes notice.***
 
***Increase speed and agility. IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes. This results in a dramatic increase in agility for the organization since the cost and time it takes to experiment and develop is significantly lower.***
 
***Stop spending money running and maintaining data centers. Focus on projects that differentiate your business, not the infrastructure. Cloud computing lets you focus on your customers, rather than on the heavy lifting of racking, stacking, and powering physical infrastructure. This is often referred to as undifferentiated heavy lifting.***

***Go global in minutes. Easily deploy your application in multiple Regions around the world with just a few clicks. This means you can provide lower latency and a better experience for your customers at a minimal cost.***


## Get started by launch your web application on Amazone EC2
### Before starting, create your own  [account](https://portal.aws.amazon.com/billing/signup#/start/email)

***VPC is a private network that make us to deploy our instance (virtual machine)***

- ### Task 1: Creating the VPC
In this task, you will create a new VPC.<br>

In the Services search box, enter VPC and open the VPC console by choosing VPC from the list.<br>

In the navigation pane, under Virtual private cloud, choose Your VPCs.<br>
Choose Create VPC, Configure these settings:
Name tag:<br>
my-vpc IPv4 [CIDR](https://letmegooglethat.com/?q=CIDR) block: 10.1.0.0/16
<br>

In the navigation pane, under Virtual private cloud, choose **internet gateways** (is like a router is not physical thing , it's just configuration , make us to connect our VPC with the World Wide Web)
<br>
Choose Create internet gateway.

<br>For Name tag, paste app-igw and choose Create internet gateway.

<br>In the details page for the internet gateway, choose Actions and then choose Attach to VPC.

<br>For Available VPCs, choose my-vpc and then choose Attach internet gateway.

- ### Task 2: Creating subnets
In this task, you will create the four [subnets](https://letmegooglethat.com/?q=subnet)<br> for your VPC. You will configure the two public subnets first, and then configure the two private subnets.
<br>
From the navigation pane, choose Subnets.
<br>

Choose Create subnet.
For the first public subnet, configure these settings:<br>
VPC ID: my-vpc
Subnet name:Public Subnet 1<br>
[Availability Zone](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html): <br>Choose the first Availability Zone
<br>Example: If you are in US West (Oregon), you would <br>choose us-west-2a
IPv4 CIDR block: 10.1.1.0/24

<br>Choose Add new subnet.
For the second public subnet, configure these settings:<br>
Subnet name: Public Subnet 2<br>
Availability Zone: Choose the second Availability Zone<br>
Example: If you are in US West (Oregon), you would choose <br>us-west-2b
IPv4 CIDR block: 10.1.2.0/24<br>
Choose Add new subnet and for the first private subnet, <br>configure these settings:
Subnet name: Private Subnet 1<br>
Availability Zone: Choose the first Availability Zone<br>
Example: If you are in US West (Oregon), you would choose<br> us-west-2a
IPv4 CIDR block: 10.1.3.0/24.
<br>Choose Add new subnet and for the second private subnet, configure the following:<br>
Subnet name: Private Subnet 2<br>
Availability Zone: Choose the second Availability Zone
Example: If you are in US West (Oregon), you would choose <br>us-west-2b
IPv4 CIDR block: 10.1.4.0/24
<br>
Finally, choose Create subnet.
<br>
After the subnets are created, select the check box for Public Subnet 1.
<br>
Choose Actions and then choose Edit subnet settings.
<br>
For Auto-assign IP settings, select Enable auto-assign public IPv4 address and then choose Save.
<br>
Clear the check box for Public Subnet 1 and select the check box for Public Subnet 2.
<br>
Again, choose Actions and then Edit subnet settings.
<br>
For Auto-assign IP settings, select Enable auto-assign public IPv4 address and save the settings.


- ### Task 3: Creating route tables
In this task, you will create the [route tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html#RouteTables) for your VPC.<br>

First, you will create the public route table.<br>

In the navigation pane, choose Route Tables.<br>

Choose Create route table.<br>
For the route table, configure these settings:<br>
Name: app-routetable-public<br>
VPC: my-vpc<br>

Choose Create route table.<br>

If needed, open the route table details pane by choosing app-routetable-public from the list.

Choose the Routes tab and choose Edit routes.<br>
Choose Add route and configure these settings:<br>
Destination: 0.0.0.0/0<br>
Target: Internet Gateway, then choose app-igw (which you set up in the VPC task)<br>

Choose Save changes.
<br>
Choose the Subnet associations tab.<br>

Scroll to Subnets without explicit associations and choose Edit subnet associations.<br>

Select the two public subnets that you created (Public Subnet 1 and Public Subnet 2) and choose Save associations.<br>

Next, you will create the private route table.<br>

In the navigation pane, choose Route Tables.<br>
Choose Create route table and configure these settings:<br>
Name: app-routetable-private<br>
VPC: my-vpc<br>

Choose Create route table.<br>

If needed, open the details pane for app-routetable-private by choosing it from the list.<br>

Choose the Subnet associations tab.<br>

Scroll to Subnets without explicit associations and choose Edit subnet associations.<br>

Select the two private subnets (Private Subnet 1 and Private Subnet 2) and choose Save associations.<br>

- ### Task 4: Launching an EC2 instance that uses a role

Now that you have created a network, you will launch your EC2 instance by using the VPC that you created!

In the search box, enter EC2 and open the Amazon EC2 console by choosing EC2 from the list.<br>

In the navigation pane, choose Instances and choose Launch instances.<br>

For Name use my-first-app-in-aws.<br>

Under Application and OS Images (Amazon Machine Image), choose Amazon Linux.<br>

Under Instance type, select t2.micro.<br>

Under Key pair (login) choose create new key pair.<br>
Configure the following settings under Network settings and Edit.<br>
VPC: my-vpc<br>
Subnet: Public Subnet 1<br>
Auto-assign Public IP: Enable<br>

Under Firewall (security groups) choose Create security group. <br>Use web-security-group as the Security group name and change Description to Enable HTTP access.
<br>
Under Inbound security groups rules choose Remove above the ssh rule.

<br>Choose Add security group rule. For Type choose HTTP. Under Source type choose Anywhere.

<br>Choose Add security group rule. For Type choose HTTPS. Under Source type choose Anywhere.

<br>Expand Advanced details and under IAM instance profile choose S3DynamoDBFullAccessRole.

In the User data box, paste the following code:
```shell
#!/bin/bash -ex [ #!/bin/bash -ex] 
wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/FlaskApp.zip [ wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/FlaskApp.zip] 
unzip FlaskApp.zip [ unzip FlaskApp.zip]  [ cd FlaskApp/] 
cd FlaskApp/
yum -y install python3 mysql
pip3 install -r requirements.txt
amazon-linux-extras install epel
yum -y install stress
export PHOTOS_BUCKET=${SUB_PHOTOS_BUCKET}
export AWS_DEFAULT_REGION=<INSERT REGION HERE>
export DYNAMO_MODE=on
FLASK_APP=application.py /usr/local/bin/flask run --host=0.0.0.0 --port=80
```
<br>

Example:

This example uses the US West (Oregon) Region, or us-west-2.
<br>
```shell
export AWS_DEFAULT_REGION=us-west-2
```
<br>

Note: You still don’t need to change the SUB_PHOTOS_BUCKET variable in the user data script, is just a bucket to store the pictures using Amazon s3 bucket service, you can create your own bucket ,[visit-this-link](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html)
Choose Launch instance.<br>

Choose View all instances.

The instance should now be listed under Instances.

Wait for the Instance state to change to Running and the Status check to change to 2/2 checks passed.

Note: Often, the status checks update, but the console user interface (UI) might not update to reflect the most recent information. You can minimize waiting by refreshing the page after a few minutes.

Select the running my-first-app-in-aws instance by selecting its check box.

On the Details tab, copy the Public IPv4 address.

Note: Make sure that you only copy the address instead of choosing the open address link.

In a new browser window, paste the IP address that you copied. Make sure to remove the ‘S’ after HTTP so you are using only HTTP instead.

In a new browser window, paste the IP address that you copied.


![aws-pic](/assets/finale.png)














