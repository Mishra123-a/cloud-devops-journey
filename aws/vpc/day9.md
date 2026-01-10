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
