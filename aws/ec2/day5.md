## EC2 Day 5 – Instance Launch Decisions & Pre-Launch Reasoning

### Objective
Understand EC2 not by launching instances blindly, but by analyzing the decisions AWS forces before an instance even exists.

### What I did
- Accessed EC2 console and studied the complete instance launch workflow
- Reviewed AMI options and compared Amazon Linux vs Ubuntu
- Analyzed instance type selection (t2.micro vs t3.micro)
- Observed how region selection affects resource scope
- Reviewed default networking and security assumptions before launch

---

### Key technical questions I asked myself
- Why does AWS separate AMI selection from instance type?
- What happens if the AMI is changed but instance type remains the same?
- Why are free-tier instances limited in performance?
- Why does region selection matter before launching anything?
- What problems can occur if instances are launched without understanding defaults?

---

### Observations & understanding gained
- AMI defines the operating system and base environment
- Instance type defines compute capacity and cost
- Region controls where compute physically runs and what resources are visible
- EC2 creation is a design decision, not just resource creation
- Default choices can lead to security, cost, or availability issues later

---

### Why this matters in real environments
In production:
- Poor AMI choice leads to maintenance issues
- Wrong instance type causes cost overruns or performance problems
- Region mistakes cause visibility and dependency issues
- Early EC2 decisions are hard to undo later


---
