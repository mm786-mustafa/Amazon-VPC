<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Muhammad Mustafa  
**Email:** pkisbim76@gmail.com

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that enables users to create isolated virtual networks within the AWS cloud, providing a secure and scalable environment for deploying resources like EC2 instances and databases. It offers enhanced security by allowing users to define their IP address range, create subnets, and configure route tables and network gateways. VPC supports security groups and network access control lists (ACLs) to regulate traffic, ensuring only authorized access. Additionally, it provides various connectivity options, such as VPN connections and AWS Direct Connect, facilitating secure communication with on-premises data centers. With its scalability and seamless integration with other AWS services, Amazon VPC is essential for businesses and developers looking for a customizable and secure cloud hosting environment.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a secure and isolated network for my EC2 instances. I configured the VPC by defining the IP address range and creating subnets, while setting up security groups and network access control lists (ACLs) to control traffic. I utilized EC2 Instance Connect for secure access to the instances and tested connectivity between them using the ping command, as well as external connectivity with curl. Overall, Amazon VPC provided a secure and organized environment, enabling seamless communication between resources while maintaining strict security measures.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was the complexity of configuring network access control lists (ACLs) alongside security groups. Initially, I thought that setting up security groups alone would be sufficient to manage traffic effectively. However, I quickly realized that the interplay between ACLs and security groups added an extra layer of complexity, as both needed to be configured correctly to ensure proper connectivity. This experience highlighted the importance of thoroughly understanding the nuances of network configurations in AWS, as even minor oversights could lead to connectivity issues.

### This project took me...

The project took me about 1 hour to complete. This included configuring the Amazon VPC, setting up EC2 instances, and testing connectivity using tools like ping and curl to ensure everything was functioning correctly.

---

## Connecting to an EC2 Instance

Connectivity means the ability of different resources within a network to communicate with each other and with external systems. In the context of a Virtual Private Cloud (VPC), it refers to how well instances, such as EC2 instances, can connect to one another and to the internet or other services. This includes ensuring that the necessary network configurations, such as security groups and network access control lists (ACLs), are correctly set up to allow or restrict traffic as intended. Effective connectivity is crucial for the proper functioning of applications and services hosted within the VPC, enabling seamless data transfer and communication.

My first connectivity test was whether I could connect to an EC2 instance within my Virtual Private Cloud (VPC). This involved using EC2 Instance Connect to establish a secure connection and verify that I could access the instance successfully. Ensuring this connectivity is essential for managing and interacting with the resources hosted on that instance.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is a feature that allows secure and easy access to EC2 instances without the need for a traditional SSH client. It enables users to connect to their instances directly from the AWS Management Console or through the AWS CLI, using temporary SSH keys. This approach simplifies the connection process, especially for instances that do not have a public IP address, and enhances security by reducing the need to manage persistent SSH keys. EC2 Instance Connect also supports IAM policies, allowing for fine-grained access control to instances based on user permissions.

My first attempt at getting direct access to my public server resulted in an error because I did not add the SSH rule in the security group. This oversight prevented the necessary inbound traffic on port 22, which is required for SSH connections. Without this rule, the connection request was blocked, leading to the failure of my initial access attempt. To resolve this issue, I needed to update the security group settings to allow SSH traffic from my IP address.

I fixed this error by updating the security group associated with my EC2 instance to allow inbound SSH traffic. Specifically, I added a rule that permitted connections on port 22 from my IP address. After applying this change, I was able to successfully connect to my public server using EC2 Instance Connect. This ensured that my connection requests were no longer blocked, allowing for secure access to the instance.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a network utility tool that sends ICMP echo request packets to a specified IP address to determine if a host is reachable and measure the round-trip time for messages. I used ping to test the connectivity between my EC2 instance and other instances within my Virtual Private Cloud (VPC), as well as to external endpoints. This helped me verify that the instances could communicate effectively and identify any network issues that might be affecting access.

The ping command I ran was 'ping <IP_ADDRESS>'. Here, <IP_ADDRESS> was the address of the EC2 instance or external endpoint I wanted to test connectivity with. This command sent ICMP echo requests to that IP address and displayed the response times and success rates, allowing me to assess the connectivity.

The first ping returned a "destination unreachable" message because I did not add the necessary ICMP rules in the Network Access Control List (NACL) and the security group associated with the private instance. This meant that the ping requests were blocked, preventing my EC2 instance from reaching the target IP address. As a result, I needed to update both the NACL and security group settings to allow ICMP traffic, enabling successful ping responses and proper communication between the instances.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshot this by reviewing the security group and Network Access Control List (NACL) settings associated with my EC2 instance. I identified that the ICMP rules were missing, which were necessary for allowing ping requests. To resolve the error, I added the appropriate inbound and outbound rules to both the security group and the NACL to permit ICMP traffic. After making these changes, I re-ran the ping command, which successfully returned responses, confirming that the connectivity issue was resolved.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is a command-line tool used for transferring data to or from a server using various protocols, including HTTP, HTTPS, FTP, and more. It allows users to make requests to web servers and retrieve information, making it useful for testing and interacting with APIs. With curl, you can send GET, POST, PUT, and DELETE requests, as well as include headers, data, and authentication credentials. It is widely used for debugging and checking the connectivity of web services and applications.

I used curl to test the connectivity between my EC2 instance and external endpoints, such as web servers or APIs. This allowed me to verify that my instance could successfully send HTTP requests and receive responses. By using curl, I could check if specific services were reachable and functioning correctly, which is essential for ensuring that applications hosted on the EC2 instance can communicate with necessary external resources. Additionally, curl provides detailed output, including response codes and headers, which aids in diagnosing any connectivity issues.

### Ping vs Curl

Ping and curl are different because they serve distinct purposes and operate at different layers of the network stack. Ping is used to test the reachability of a host by sending ICMP echo request packets, determining if a target IP address is reachable and measuring round-trip time. It provides basic connectivity information about whether the host is up or down. In contrast, curl is a command-line tool that transfers data to or from a server using protocols like HTTP and FTP. It allows users to send specific requests (GET, POST, PUT, DELETE) to web servers, enabling interaction with APIs and retrieval of detailed responses. While ping checks basic connectivity, curl offers more comprehensive information about service functionality.

---

## Connectivity to the Internet

I ran the curl command `curl example.com`, which returned the HTTP headers from the server. This included information such as the HTTP status code, server type, and content type. The response confirmed that the server was reachable and functioning correctly, indicating successful connectivity between my EC2 instance and the external web server. The status code returned was `200 OK`, which signifies that the request was successful and the server was able to process it.

![Image](http://learn.nextwork.org/excited_gray_glamorous_dog/uploads/aws-networks-connectivity_8ee57662)

---

---
