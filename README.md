🌐 AWS VPC Peering Project (Test ↔ Prod)
📌 Project Overview

This project demonstrates VPC Peering connectivity between two Virtual Private Clouds (VPCs) named Test and Prod using route tables, Internet Gateway (IGW), and NAT Gateway.
The architecture enables secure private communication between VPCs while allowing controlled internet access.

🏗️ Architecture Summary
🔹 VPCs

Test VPC

Prod VPC

Both VPCs are created with non-overlapping CIDR blocks to allow peering.

🔹 Subnets
Prod VPC

Public Subnet

EC2 Instance

Internet access via Internet Gateway

Private Subnet

EC2 Instance

Internet access via NAT Gateway (through public subnet)

Test VPC

Subnet(s) with EC2 Instance(s)

🔹 Gateways

Internet Gateway (IGW)

Attached to Prod VPC

Provides internet access to public subnet

NAT Gateway

Deployed in Prod public subnet

Allows private subnet instances to access the internet securely

🔹 VPC Peering

Peering connection established between Test VPC and Prod VPC

Enables private IP communication between EC2 instances across both VPCs

Traffic flows using route table entries, not via internet

🗺️ Route Table Configuration
📍 Prod Public Subnet Route Table
Destination	Target
0.0.0.0/0	Internet Gateway
Test VPC CIDR	VPC Peering Connection
📍 Prod Private Subnet Route Table
Destination	Target
0.0.0.0/0	NAT Gateway
Test VPC CIDR	VPC Peering Connection
📍 Test VPC Route Table
Destination	Target
Prod VPC CIDR	VPC Peering Connection
🔐 Security Configuration

Security Groups

Allow required inbound traffic (SSH / ICMP / Application ports)

Network ACLs

Allow traffic between Test and Prod CIDR ranges

No transitive routing (VPC Peering limitation respected)

✅ Features & Benefits

✔ Secure private communication between Test and Prod environments

✔ Internet access only through controlled gateways

✔ Separation of public and private resources

✔ Cost-effective and low-latency VPC connectivity

✔ Real-world enterprise network design

🧪 Validation & Testing

Ping / SSH from Test VPC EC2 to Prod VPC EC2 using private IP

Internet access tested:

Public subnet → via IGW

Private subnet → via NAT Gateway

Verified route table entries and peering status

🚀 Use Cases

Environment separation (Dev/Test ↔ Prod)

Microservices communication

Hybrid cloud architecture preparation

Secure backend connectivity

📘 Conclusion

This project successfully implements AWS VPC Peering using route tables, Internet Gateway, and NAT Gateway, ensuring secure, scalable, and production-ready network communication between isolated VPCs.
