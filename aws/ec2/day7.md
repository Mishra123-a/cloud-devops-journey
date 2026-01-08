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

