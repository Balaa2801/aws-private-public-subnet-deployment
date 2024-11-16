# aws-private-public-subnet-deployment
****AWS Private and Public Subnet Application Deployment**

**Project Overview**

This project demonstrates how to deploy a simple web application on AWS by creating a VPC with both private and public subnets. It walks through configuring EC2 instances in private subnets, using a Bastion host for secure access, and deploying an application behind a Load Balancer to ensure traffic is distributed across two EC2 instances.

**Architecture**

VPC with Public and Private Subnets: The VPC includes both private subnets for application instances and public subnets for NAT and Bastion hosts.
Auto Scaling Group: Automatically adjusts the number of instances based on demand.
Bastion Host: Provides SSH access to the private EC2 instances.
Load Balancer: Distributes incoming HTTP traffic across the EC2 instances.
EC2 Instances: Hosts the web application.

**Steps Taken**

**Create a VPC**

First, created a new VPC to host both private and public subnets. This also included setting up the necessary internet and NAT gateways for secure communication.

**Launch EC2 Instances in Private Subnets**

Created two EC2 instances within private subnets using an Auto Scaling Group and a Launch Template.
The instances will be automatically scaled based on load.

**Set Up Bastion Host**

Created a Bastion host in a public subnet to allow SSH access to private instances.
Transferred the key pair from my local machine to the Bastion host using scp command.

**SSH into Private Instances**

Used the Bastion host to SSH into the private EC2 instances via their private IPs.
Created a simple index.html on the private instances and hosted it using Python’s HTTP server:
bash
Copy code
python3 -m http.server 8000

**Set Up Load Balancer**
Created a target group for the Load Balancer to manage HTTP traffic distribution.
Configured the Load Balancer to distribute traffic between the EC2 instances.
Updated the Security Group to allow HTTP traffic on port 80 to the Load Balancer.

**Update Security Group Rules**

Initially, the Load Balancer did not allow HTTP traffic on port 80. After modifying the security group to allow HTTP traffic, the setup was functional.

**Test the Application**

The Load Balancer's DNS link was copied and pasted into the browser, where the index.html page hosted on the EC2 instances was successfully accessed.

Configured the second EC2 instance in a similar manner, changing the index.html content to differentiate the projects.

**Load Balancer Traffic Distribution**

Once both instances were running, the Load Balancer successfully distributed traffic between them, demonstrating high availability.

**Conclusion**

This project demonstrates deploying a simple web application in AWS using private and public subnets with Auto Scaling, a Bastion host for secure access, and a Load Balancer for traffic distribution.

**Screenshots**

I have uploaded all the screenshots related to this project in the folder named "Aws-Project-Screenshots." Please refer to this folder for visual aids and additional details of the steps mentioned above.

**Future Enhancements**

Automating the infrastructure deployment using Terraform.

Implementing CloudWatch for monitoring and alerts.

Integrating CI/CD pipelines to automate application deployment.
