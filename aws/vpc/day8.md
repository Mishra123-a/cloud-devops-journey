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


