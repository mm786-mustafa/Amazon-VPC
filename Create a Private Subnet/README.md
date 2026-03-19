<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Muhammad Mustafa  
**Email:** pkisbim76@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that allows users to create a logically isolated section of the Amazon Web Services (AWS) cloud where they can launch AWS resources in a virtual network that they define. This includes control over the IP address range, subnets, route tables, and network gateways.

It is useful because it provides users with enhanced security and control over their cloud resources. By allowing the creation of private and public subnets, users can segment their applications and data based on security needs. Additionally, VPC enables fine-grained control over network traffic through features like security groups and network ACLs, ensuring that sensitive data is protected while still allowing necessary access to resources. This level of customization helps organizations meet compliance requirements and optimize their network architecture for performance and security.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a secure and isolated virtual network for hosting my cloud resources. This included defining the IP address range, creating public and private subnets, and setting up routing tables to control traffic flow. By utilizing private subnets, I ensured that sensitive resources, such as databases and application servers, were protected from direct internet access.

I configured a dedicated route table for the private subnet to manage internal communications effectively and established a dedicated Network Access Control List (NACL) to refine access controls, allowing only specific IP addresses to communicate with the instances. This setup enhanced security and improved management of network traffic, meeting both operational needs and compliance requirements.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was the complexity involved in configuring the network settings for the private subnet. Initially, I assumed that setting up a Virtual Private Cloud (VPC) would be straightforward, but I encountered various challenges related to IP address management, route table configurations, and ensuring proper access controls with Network Access Control Lists (NACLs). The need for careful planning and attention to detail in defining the CIDR blocks and managing traffic flow was more intricate than I anticipated. This experience highlighted the importance of understanding network architecture and security best practices when working with cloud infrastructure.

### This project took me...

This project took me about 1 hour to complete. I spent this time configuring the Amazon VPC components, including subnets, route tables, and network ACLs, while troubleshooting various issues. The process involved careful planning and testing to ensure all resources operated securely and efficiently, making it a valuable learning experience.

---

## Private vs Public Subnets

The difference between public and private subnets is that public subnets are designed to host resources that require direct access to the internet, such as web servers or load balancers. These resources have public IP addresses and can communicate directly with the outside world. In contrast, private subnets are intended for resources that do not need direct internet access, such as databases or application servers. These resources typically have private IP addresses and can communicate with other resources within the VPC but are isolated from direct internet traffic, enhancing security and control over data flow.

Having private subnets is useful because they provide an additional layer of security for sensitive resources within a Virtual Private Cloud (VPC). By isolating these resources from direct internet access, private subnets help protect them from potential external threats and unauthorized access. This is particularly important for databases, application servers, and other critical infrastructure that should not be exposed to the public internet. Additionally, private subnets allow for better network management and control, enabling organizations to implement specific security measures, such as firewalls and access control lists, to regulate traffic flow and enhance overall security posture.

My private and public subnets cannot have the same IP address range. Each subnet within a Virtual Private Cloud (VPC) must have a unique CIDR block to ensure that there are no overlapping IP addresses. This distinction is crucial for proper routing and communication between resources within the VPC, as it prevents conflicts and ensures that each subnet can operate independently while still allowing for controlled interaction when necessary.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the main route table of the Virtual Private Cloud (VPC). This main route table controls the routing for all subnets that do not have an explicitly defined route table. However, to optimize security and traffic management, it is recommended to create a dedicated route table specifically for the private subnet. This allows for more granular control over the routing rules and ensures that the private subnet operates according to the specific needs of the resources within it, particularly in terms of internet access and inter-subnet communication.

I had to set up a new route table because the default main route table does not provide the necessary control and security for my private subnet. By creating a dedicated route table, I can customize the routing rules specifically for the resources within the private subnet, ensuring that they can communicate effectively while remaining isolated from direct internet access. This setup enhances security by allowing me to define specific routes for internal communication and manage traffic flow more efficiently, ultimately improving the overall performance and security posture of my Virtual Private Cloud (VPC).

My private subnet's dedicated route table only has one inbound and one outbound rule that allows traffic between the resources within the private subnet. The inbound rule permits traffic from other instances within the same subnet, facilitating communication for applications and services that need to interact with each other. The outbound rule allows traffic to flow to other resources in the VPC, ensuring that the private subnet can access necessary services while still maintaining its isolation from the public internet. This configuration enhances security by limiting external access while enabling essential internal communications.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the main Network Access Control List (NACL) of the Virtual Private Cloud (VPC). This main NACL applies to all subnets that do not have a specific NACL assigned to them. While this default NACL allows all inbound and outbound traffic, it is advisable to create a dedicated NACL for the private subnet. This allows for more granular control over the traffic rules, enhancing security by enabling specific allow or deny rules tailored to the needs of the resources within the private subnet.

I set up a dedicated network ACL for my private subnet because the default main Network Access Control List (NACL) does not provide the level of security and control that my private subnet requires. By creating a dedicated NACL, I can define specific inbound and outbound rules tailored to the needs of the resources within the private subnet. This allows me to restrict access to only authorized traffic, thereby enhancing security and protecting sensitive resources from potential threats. Additionally, a dedicated NACL enables better management of traffic flow, ensuring that only necessary communications are permitted while maintaining isolation from the public internet.

My new network ACL has two simple rules. The inbound rule allows traffic from specific IP addresses or ranges authorized to access resources within the private subnet, ensuring that only trusted sources can communicate with instances in the subnet. The outbound rule permits traffic to specific IP addresses or ranges, enabling the resources within the private subnet to communicate with necessary services or instances while maintaining control over what can exit the subnet. These rules are designed to enhance security by tightly controlling both incoming and outgoing traffic, ensuring that only authorized communications are permitted while keeping the private subnet isolated from unwanted external access.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-private_1ed2cb07)

---

---
