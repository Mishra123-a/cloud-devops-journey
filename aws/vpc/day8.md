## Why VPC Exists

Before VPC, AWS customers had very limited control over networking.  
Instances were launched into shared infrastructure with minimal isolation and customization.

VPC was introduced to solve the following problems:
- Lack of network isolation
- No control over IP address ranges
- No control over routing and internet access
- Difficulty designing secure architectures

A VPC allows customers to build a **private, isolated network inside AWS**, similar to a traditional data center network.

---

## What a VPC Actually Is

A VPC is a **logically isolated virtual network** within AWS.

It represents:
- A private IP address space
- A controlled networking boundary
- The foundation where AWS resources are deployed

A VPC itself does **not run applications**.  
It only provides the **networking environment**.

---
## VPC Lifecycle (High-Level)

1. A VPC is created with a CIDR block
2. Subnets are created inside the VPC
3. Route tables are configured
4. Gateways (Internet / NAT) are attached if required
5. Resources like EC2 are launched inside subnets
6. The VPC continues to exist until manually deleted

A VPC does not automatically scale or terminate.

---

## CIDR and IP Address Ranges

When creating a VPC, an IP address range must be defined using **CIDR notation**.
Example -  10.0.0.0/16
This CIDR block:
- Defines the total IP space for the VPC
- Controls how many IP addresses are available
- Cannot be changed after creation

All subnets and resources must use IPs from this range.

---

## Subnets

A subnet is a **smaller IP range inside a VPC**.

Subnets are used to:
- Organize resources
- Separate workloads
- Map resources to Availability Zones

Important rules:
- Each subnet belongs to **one VPC**
- Each subnet belongs to **one Availability Zone**
- Subnet CIDR must be a subset of the VPC CIDR

---
## Public and Private Subnets

Subnets are not public or private by default.  
They become public or private **based on routing**.

no

## Public and Private Subnets

Subnets are not public or private by default.  
They become public or private **based on routing**.

### Public Subnet

A subnet is considered public when:
- Its route table has a route to an Internet Gateway

Typical use cases:
- Load balancers
- Bastion hosts
- Public-facing services

### Private Subnet

A subnet is considered private when:
- It does not have a direct route to the Internet Gateway

Typical use cases:
- Application servers
- Databases
- Internal services

---

## Route Tables

A route table defines **how traffic flows** within and outside the VPC.

Each subnet must be associated with a route table.

Route tables determine:
- Whether traffic stays inside the VPC
- Whether traffic goes to the internet
- Whether traffic goes through NAT or VPN

Routing is what actually enforces network behavior.

---

## Internet Gateway (IGW)

An Internet Gateway enables communication between the VPC and the internet.

Key points:
- Only one Internet Gateway can be attached to a VPC
- It must be explicitly attached
- A subnet becomes public only when its route table sends traffic to the IGW

The IGW alone does not expose resources.  
Routing and security rules must allow access.

---

## NAT (Conceptual Overview)

NAT is used when:
- Instances in private subnets need outbound internet access
- Inbound internet access should remain blocked

NAT allows:
- Private → Internet traffic
- Blocks Internet → Private traffic

This is commonly required for updates and external API calls.

---
### Security Groups
- Stateful virtual firewalls
- Control inbound and outbound traffic at the resource level
- Applied to ENIs, not subnets

---
### Network ACLs (NACL)
- Stateless subnet-level traffic filters
- Apply to all resources in a subnet
- Evaluated in order using rule numbers

---
### VPC Peering
- Private connectivity between VPCs
- Requires non-overlapping CIDR ranges
- No transitive routing

---

### VPC Endpoints
- Private access to AWS services without internet
- Keeps traffic inside AWS network
- Used for security and compliance

---

### Bastion Host
- Publicly accessible EC2 used for administrative access
- Acts as a controlled entry point to private resources
- Requires strict security group rules

---
### Elastic IP
- Static public IP owned by the AWS account
- Survives stop/start of instances
- Solves IP stability, not availability

---

### VPC Flow Logs
- Capture network traffic metadata
- Used for troubleshooting and security analysis
- Does not capture packet payloads

---
## Practical Work Performed

### VPC & Subnet Creation
- Created a custom VPC with defined CIDR range
- Created subnets inside the VPC
- Understood AZ-specific nature of subnets

---

### Route Table Configuration
- Created a custom route table
- Manually associated subnets with the route table
- Verified subnet-to-route-table relationship

---

### Internet Gateway Integration
- Created and attached an Internet Gateway to the VPC
- Added default route (0.0.0.0/0) pointing to IGW
- Enabled internet connectivity for public subnet

---

## Key Learnings
- Subnets are public or private based on routing, not naming
- Route tables control traffic flow, not security groups
- Internet access requires correct combination of:
  - IGW
  - Route table
  - Subnet association
- Many VPC components are architectural, not always directly visible in labs

---
### AWS Direct Connect
- Dedicated private network connection to AWS
- Reduces latency and improves bandwidth consistency
- Used for hybrid enterprise architectures

---
