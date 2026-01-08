## EC2 Day 4 – What EC2 Really Is, Lifecycle Behavior & Failure Thinking

### Objective
Understand EC2 from a **system and failure perspective**, not myths or assumptions.
This write-up focuses on what EC2 actually provides — and what it does NOT.

---

## What EC2 Really Is ??

Amazon EC2 is simply a **virtual machine** running on AWS-managed physical hardware.

An EC2 instance consists of:
- CPU
- Memory (RAM)
- Storage (disk)
- Network interface

AWS owns and manages the physical infrastructure.
I rent virtual compute capacity.

Important clarification:
EC2 **by itself** does NOT provide:
- High availability
- Auto-healing
- Zero downtime

Those capabilities come from **architecture**, not EC2 alone.

---
## EC2 Lifecycle – Real Behavior

### Reboot
- Equivalent to an OS restart
- No infrastructure-level changes
- Public IP remains the same
- Private IP remains the same
- EBS storage remains intact

Used for:
- OS updates
- Application restarts

---

### Stop / Start
- Instance is powered off and later powered on
- Root and additional EBS volumes remain intact
- **Public IP changes** (unless Elastic IP is attached)
- **Instance Store data is lost**

Used for:
- Cost saving
- Instance resizing
- Maintenance

---

### Terminate
- Instance is permanently destroyed
- Root EBS volume is deleted by default
- Additional EBS volumes may survive (based on configuration)
- No recovery unless backups exist

Termination means compute is gone forever.

---


