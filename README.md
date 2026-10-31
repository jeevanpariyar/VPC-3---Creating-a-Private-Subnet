## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to create a Private Subnet .I'm doing this project to learn private subnet creation , Private RouteTable , and more.

### ✍️ What are we doing in this step?

In this step, I will  be craeting below resources.

Create a VPC.\
Create subnets.\
Create an internet gateway.\
Create a route table.\
Create a security group.\
Create a network ACLs.

### ✍️ What are we doing in this step?

In this step, We set up your very first private subnet and learn its differences from a public subnet along the way.  because critical Resource on cloud are never exposed directly to Internet ,so we create a  private subnet and place the Resources in it.

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is an AWS service that allows you to create a logically isolated virtual network in the AWS Cloud to launch and manage resources such as EC2 instances and databases.

Why is it useful?

\- Security: Control network traffic using security groups and Network ACLs (NACLs).\
\- Network isolation: Keep AWS resources within a logically isolated network.\
\- IP management: Define IP address ranges using CIDR blocks.\
\- Traffic routing: Control network traffic using route tables, Internet Gateways, and NAT Gateways.\
\- Flexible architecture: Create public and private subnets to separate internet-facing applications from internal resources.

### How I used Amazon VPC in this project

In today's project, I created an Amazon VPC and configured public and private subnets, route tables, and an Internet Gateway. I also configured security groups and created a custom Network ACL (NACL) to control inbound and outbound traffic at the subnet level. This hands-on project helped me understand how to design a secure AWS network, manage traffic flow, and protect cloud resources from unauthorized access.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that Network ACLs are stateless, meaning I must configure both inbound and outbound rules to allow request and response traffic. I learned that NACLs provide an additional layer of security at the subnet level, while security groups protect individual resources such as EC2 instances.

### This project took me...

This project took me around 30 -45 minutes.

## Private vs Public Subnets

Public Subnet: A subnet whose route table has a route to an Internet Gateway (IGW). Resources can communicate directly with the internet if they have a public IP address and the required security rules.

Private Subnet: A subnet whose route table does not have a direct route to an Internet Gateway. Resources can access the internet through a NAT Gateway if configured, without being directly reachable from the internet.

Example: A public subnet hosts a web server, while a private subnet hosts an application server or database to improve security.

Private subnets exist to protect sensitive AWS resources from direct access from the public internet. They are used to host databases, application servers, and internal services that should not be directly reachable from the internet. They improve security by controlling network traffic through route tables, security groups, and NACLs while allowing necessary communication with other resources in the VPC.

Public and private subnets cannot share the same IPv4 CIDR block or overlapping IP address ranges within a VPC. Each subnet must have a unique, non-overlapping CIDR block.\
They can share the same VPC, but they can use different route tables and security configurations to control network traffic.

### ✍️ What are we doing in this step?

In this step, I will create a private subnet also needs to be associated with a route table.

![Private vs Public Subnets](https://nextwork.ai/intense_gray_jolly_kokako/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_afe1fdbd)

## A dedicated route table

NextWork route table is the default route table for your entire VPC. Subnets that aren't associated with another route table automatically use NextWork route table.

I am setting up a new route table to control how network traffic flows from my subnet to other networks. It allows me to define custom routes, associate the route table with the appropriate subnet, and control internet connectivity through an Internet Gateway or NAT Gateway. This helps separate public and private subnet traffic and improves network security in my Amazon VPC.

My private subnet's dedicated route table only has one inbound and one outbound rule that allows local routing within the subent .

### ✍️ What are we doing in this step?

In this step, I will create and configure a Network Access Control List (NACL) for the private subnet in my Amazon VPC. A NACL acts as a subnet-level firewall that controls inbound and outbound traffic using allow and deny rules. This helps add an extra layer of security to protect private resources from unauthorized network access.

![A dedicated route table](https://nextwork.ai/intense_gray_jolly_kokako/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_b4b904b5)

## A new network ACL

By default, the private subnet is associated with the default Network ACL (NACL) of the VPC, unless a custom NACL has been explicitly associated with it. The default NACL allows all inbound and outbound traffic by default.

I am setting up a new Network ACL (NACL) to add an extra layer of security to my private subnet. It allows me to define custom inbound and outbound rules to control network traffic, block unauthorized access, and protect private resources such as application servers and databases.

Inbound rules: Allow traffic from trusted sources on required ports, such as SSH (port 22) from an authorized IP range and application traffic from the public subnet.

Outbound rules: Allow required outgoing traffic, including responses to permitted inbound connections and communication with approved resources.

Since NACLs are stateless, both inbound and outbound rules must be configured explicitly, including return traffic on the required ephemeral ports. All other traffic is denied by default unless an earlier matching rule allows it.

![A new network ACL](https://nextwork.ai/intense_gray_jolly_kokako/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_1ed2cb07)
