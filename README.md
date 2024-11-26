# AWS Private and Public Subnet Application Deployment

## Project Overview

This project demonstrates the deployment of a simple web application on AWS by creating a VPC with both private and public subnets. It includes configuring EC2 instances in private subnets, using a Bastion host for secure access, and deploying the application behind a Load Balancer to ensure traffic distribution across two EC2 instances.

---

## Architecture

1. **VPC with Public and Private Subnets**:  
   - The VPC includes private subnets for application instances and public subnets for NAT and Bastion hosts.

2. **Auto Scaling Group**:  
   - Automatically adjusts the number of instances based on demand.

3. **Bastion Host**:  
   - Provides SSH access to the private EC2 instances.

4. **Load Balancer**:  
   - Distributes incoming HTTP traffic across the EC2 instances.

5. **EC2 Instances**:  
   - Hosts the web application.

---

## Steps Taken

### 1. Create a VPC
- Created a new VPC to host both private and public subnets.  
- Set up the necessary Internet and NAT Gateways for secure communication.

### 2. Launch EC2 Instances in Private Subnets
- Created two EC2 instances within private subnets using an Auto Scaling Group and a Launch Template.
- Instances automatically scale based on load.

### 3. Set Up Bastion Host
- Created a Bastion host in a public subnet to allow SSH access to private instances.  
- Transferred the key pair from the local machine to the Bastion host using the `scp` command.

### 4. SSH into Private Instances
- Used the Bastion host to SSH into private EC2 instances via their private IPs.  
- Created a simple `index.html` on the private instances and hosted it using Python’s HTTP server:  
  ```bash
  python3 -m http.server 8000

### 5. Set Up Load Balancer

- Created a Target Group for the Load Balancer to manage HTTP traffic distribution.
- Configured the Load Balancer to distribute traffic between EC2 instances.
- Updated the Security Group to allow HTTP traffic on port 80 to the Load Balancer.

---

### 6. Update Security Group Rules

- Initially, the Load Balancer did not allow HTTP traffic on port 80.
- Modified the Security Group to allow HTTP traffic, making the setup functional.

---

### 7. Test the Application

- Copied the Load Balancer's DNS link and accessed it in a browser.
- Verified that the `index.html` page hosted on the EC2 instances was accessible.

---

### 8. Configure the Second EC2 Instance

- Updated the `index.html` content on the second EC2 instance to differentiate the projects.
- Verified that the Load Balancer successfully distributed traffic between both instances.

---

## Conclusion

This project demonstrates the deployment of a simple web application in AWS using:

- Private and public subnets
- Auto Scaling
- A Bastion host for secure access
- A Load Balancer for traffic distribution

---

## Screenshots

All project-related screenshots are available in the folder named **"AWS-Project-Screenshots"**.  
Please refer to this folder for visual aids and additional details of the steps mentioned above.

---

## Future Enhancements

1. Automating the infrastructure deployment using Terraform.
2. Implementing CloudWatch for monitoring and alerts.
3. Integrating CI/CD pipelines to automate application deployment.
