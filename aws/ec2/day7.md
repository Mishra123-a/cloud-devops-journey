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

## Storage Thinking – Critical Separation

### Root EBS
- Contains operating system
- Persistent across stop/start
- Deleted on termination by default
- Not ideal for application data

---

### Additional EBS Volumes
- Used for application and data storage
- Independent of EC2 lifecycle
- Survive stop/start
- Preferred location for persistent data

---

### Instance Store
- Temporary (ephemeral) storage
- Data is lost on:
  - Stop
  - Terminate
  - Host failure
- Must never be used for critical data

---
## Networking & IP Address Logic

### Private IP
- Used inside AWS network
- Stable identity for the instance
- Does NOT change on stop/start

---

### Public IP
- Ephemeral by default
- Changes on stop/start
- Not suitable as a stable endpoint

---

### Elastic IP
- Provides a static public IP
- Survives stop/start
- Solves IP stability
- Does NOT solve availability

---

## Data vs Availability vs Recovery (Most Important Concept)

These are **three different problems** and must not be confused.

### Data Persistence
- Solved using EBS and snapshots
- Prevents data loss
- Does NOT prevent downtime

---

### Availability
- Requires multiple running instances
- Requires load balancing
- Prevents downtime

---

### Recovery
- Uses AMIs and automation
- Reduces restore time
- Still involves downtime

Confusing these leads to poor architecture decisions.

---


### Key principle
**Storage must outlive compute.**

---

