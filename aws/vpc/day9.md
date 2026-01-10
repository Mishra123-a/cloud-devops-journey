## VPC Day 1 – Region, AZ, Subnets & High Availability

### Objective
Develop a clear and correct understanding of how AWS Regions, Availability Zones, VPCs, and Subnets relate to each other, 
and how High Availability (HA) actually works in real architectures.

This write-up focuses on **eliminating common misconceptions**.

---

## 1. Region, AZ, and VPC – Clear Separation

### Region
A Region is a **geographic location**, such as:
- Mumbai
- Frankfurt
- North Virginia

A Region contains **multiple Availability Zones (AZs)**.

---
### Availability Zone (AZ)
An AZ is a **physically separate data center**.

Each AZ has:
- Independent power
- Independent cooling
- Independent networking

AZs are designed to **fail independently**.

Failure of one AZ does NOT imply failure of another AZ in the same region.

---
## 2. Subnets – Where Logic Meets Physical Reality

A subnet is **AZ-specific**.

Key characteristics:
- One subnet belongs to **only one AZ**
- A subnet cannot span multiple AZs
- Subnets are used to place resources in a specific AZ

---

### Typical Multi-AZ Subnet Layout

- Public Subnet – AZ-1  
- Private Subnet – AZ-1  
- Public Subnet – AZ-2  
- Private Subnet – AZ-2  

This layout allows applications to run in multiple AZs simultaneously.

---
### Important Reality
Multiple subnets in the **same AZ** do **NOT** provide High Availability.

---

## 3. Wrong vs Correct Subnet Design

### ❌ Wrong Design
- 4 subnets
- All subnets placed in **AZ-1**

Result:
- AZ-1 failure = complete outage
- No High Availability
- Equivalent to a single on-prem data center

---

### ✅ Correct Design
- Subnets distributed across **AZ-1 and AZ-2**
- Same subnet roles exist in each AZ

Result:
- AZ failure is survivable
- Remaining AZ continues serving traffic
- True High Availability

---


