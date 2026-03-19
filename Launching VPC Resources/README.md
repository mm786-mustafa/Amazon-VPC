<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-ec2)

**Author:** Muhammad Mustafa  
**Email:** pkisbim76@gmail.com

---

## Launching VPC Resources

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that allows users to create a logically isolated section of the AWS cloud to launch and manage resources in a virtual network. It is useful because it provides complete control over network configurations, including IP address ranges, subnets, and security features, enabling organizations to customize their architecture for security, compliance, and operational needs while facilitating secure communication between AWS resources.

### How I used Amazon VPC in this project

I used Amazon VPC to create a secure and isolated virtual network for launching and managing my AWS resources. This involved setting up both public and private subnets within the VPC, allowing me to control network configurations and access. I configured security groups to manage inbound and outbound traffic, ensuring that my public servers could communicate with the internet while keeping my private servers hidden and secure. Additionally, I utilized NAT gateways to enable outbound internet access for the private instances without exposing them to direct inbound traffic. This setup facilitated efficient resource management, enhanced security, and ensured high availability across different Availability Zones.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was the complexity of configuring security groups and network access controls. Initially, I thought it would be straightforward to allow access to my resources, but I quickly realized the importance of carefully managing inbound and outbound rules to maintain security. Balancing accessibility for necessary services while ensuring that unauthorized access was prevented required more attention and planning than I anticipated. This experience highlighted the critical role of network security in cloud architecture and the need for thorough testing to ensure everything functioned as intended.

### This project took me...

This project took me approximately 1 hours to complete. The time was spent on various tasks, including designing the VPC architecture, configuring subnets and security groups, setting up EC2 instances, and testing connectivity. Additionally, I devoted time to researching best practices for security and access management, as well as troubleshooting any issues that arose during the setup process. Overall, the project was a valuable learning experience that required careful planning and execution.

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means establishing a direct connection to the instance without intermediary services. For Amazon EC2 instances, this typically involves using Secure Shell (SSH) for Linux-based instances or Remote Desktop Protocol (RDP) for Windows-based instances. This access allows users to interact with the operating system, manage applications, and perform administrative tasks directly on the virtual machine. Direct access is essential for configuration, troubleshooting, and maintenance, enabling users to fully utilize the capabilities of their EC2 instances. By setting up secure methods like key pairs, users can ensure that this access is both convenient and protected from unauthorized use.

### SSH is a key method for directly accessing a VM

SSH traffic means the encrypted flow of data between a local computer and a remote server, acting as a secure "armored tunnel" that protects sensitive commands and login credentials from being intercepted over the public internet. By verifying that a user's private key matches the public key on the server, SSH ensures only authorized developers can gain direct access to troubleshoot or configure an instance. While it is common to leave HTTP traffic open to the world (0.0.0.0/0) for public websites, AWS provides a warning for SSH because leaving Port 22 open to all IP addresses creates a major security risk; therefore, you should always restrict SSH access to specific, known IP addresses to shield your private infrastructure.

### To enable direct access, I set up key pairs

Key pairs are a set of cryptographic keys used to secure access to Amazon EC2 instances. Each key pair consists of a public key and a private key. The public key is stored on the instance, allowing the server to identify and authenticate users attempting to connect. In contrast, the private key is securely kept by the user and is essential for establishing a secure connection to the instance. When connecting via SSH, the private key proves the user's identity, ensuring that only authorized individuals can access the server. Key pairs are crucial for maintaining security while enabling convenient access to virtual machines.

A private key's file format refers to the structure and encoding used to store the private key data, which is essential for its proper use by software or services. Common formats include PEM (Privacy-Enhanced Mail), DER (Distinguished Encoding Rules), and PPK (PuTTY Private Key). My private key's file format was "PEM", which is widely used in applications like AWS due to its base64 encoding and clear header and footer lines, ensuring compatibility with SSH clients and tools for secure connections.

---

## Launching a public server

I had to change my EC2 instance's networking settings by modifying the security group associated with the instance. This involved adding inbound rules to allow traffic on specific ports, such as port 22 for SSH access and port 80 for HTTP access. Additionally, I ensured that the subnet where the instance resides is configured to allow public access, which included associating an Elastic IP address if necessary. These changes enabled me to access the instance directly from the internet while maintaining security protocols to protect it from unauthorized access.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because it requires much stricter access controls than a public-facing server. While a public server is designed to accept HTTP traffic from the entire internet (0.0.0.0/0), a private server is meant to be hidden from the open web to minimize security risks. By using a separate security group, you can restrict SSH access so it only accepts connections originating from the NextWork Public Security Group rather than any IP address on Earth. This creates a layered defense where your private instance is completely invisible to the public internet, ensuring that only trusted resources within your own network can communicate with it.

My private server's security group's source is the NextWork Public Security Group, which means that only resources belonging to that specific group—rather than the entire internet—can communicate with the private instance. Instead of leaving the "front door" open to any IP address (0.0.0.0/0), you have restricted access to a small, trusted circle of your own public-facing resources. This creates a secure, layered architecture where an external user must first pass through your public server before they can even attempt to reach the private one, effectively shielding your most sensitive data from public scans and brute-force attacks.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

To set up my new Amazon VPC, I logged into the AWS Management Console and created a new VPC with a specified IPv4 CIDR block. I configured both public and private subnets, assigning them appropriate CIDR blocks. An Internet Gateway was created and attached to the VPC, with the public subnet's route table updated to direct traffic to it. I established security groups with specific rules to control access, allowing HTTP and SSH for the public subnet while restricting the private subnet's access. After launching EC2 instances in both subnets and assigning an Elastic IP to the public instance, I verified that the public instance was accessible and that the private instance could only be reached from the public instance, ensuring a secure and efficient VPC setup.

A VPC resource map visually represents the components and configurations within an Amazon Virtual Private Cloud (VPC). It includes public and private subnets with their CIDR blocks, route tables for traffic direction, Internet Gateways for internet communication, and security groups that control access. The map also shows the placement of EC2 instances and any assigned Elastic IP addresses. This visualization helps in managing the network architecture, troubleshooting issues, and planning for scalability and security enhancements.

My new VPC has a CIDR block of `10.0.0.0/16`. It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because they are located in different regions or accounts. Amazon Web Services (AWS) allows the reuse of CIDR blocks across different VPCs as long as they do not overlap within the same region or account. This flexibility enables organizations to create multiple VPCs for various environments (such as development, testing, and production) without the need for unique CIDR blocks for each VPC, simplifying network management and resource allocation.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options: one public subnet or two public subnets. This was because AWS recommends that each Availability Zone (AZ) in a region should have its own public subnet for redundancy and high availability. Since my VPC is configured across two Availability Zones, I chose to create two public subnets to ensure that if one AZ experienced an outage, the other could still handle traffic, thereby enhancing the overall resilience and reliability of my infrastructure.

NAT gateways are managed network address translation services provided by Amazon Web Services (AWS) that enable instances in a private subnet to access the internet while preventing inbound internet traffic from directly reaching those instances. The setup page also offered to create NAT gateways, which are essential for allowing private resources to download software updates, access external APIs, or connect to other services without exposing them to the public internet. This helps maintain security by keeping the private instances isolated while still enabling necessary outbound internet connectivity. NAT gateways are highly available and automatically scale to accommodate the traffic needs of your applications.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-ec2_8ee57662)

---

---
