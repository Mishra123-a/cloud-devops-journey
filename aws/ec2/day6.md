### SSH validation & access testing
- Verified OS-level user after SSH
- Confirmed private IP vs public access path
- Used instance metadata to validate EC2 identity
- Tested Security Group impact by removing SSH rule
- Confirmed SG controls network access, not SSH itself

## Why production avoids default public IPs

### Default EC2 public IP behavior
- By default, EC2 instances receive an **ephemeral public IPv4**
- This public IP:
  - Changes when an instance is **stopped and started**
  - Is released back to AWS when the instance stops
- Private IP remains **unchanged** inside the VPC

This makes default public IPs unreliable for production systems.

---

## Why Elastic IP is used in production

Elastic IP (EIP) is a **static, account-owned public IPv4 address**.

### Key characteristics
- Does NOT change on stop/start
- Can be reattached to another instance
- Provides a stable public endpoint

### Production use cases
- Bastion hosts
- Legacy systems requiring fixed IP allowlists
- Controlled administrative access

### Limitations
- Still tied to a single instance
- No automatic failover
- Not suitable for scalable applications

Elastic IP solves **stability**, not **availability**.

---

## Why Load Balancers are preferred in production

Load Balancers provide:
- A stable DNS endpoint
- Automatic health checks
- Traffic distribution across instances
- Integration with Auto Scaling

### Production advantages
- No dependency on EC2 public IPs
- Instances can be replaced freely

## EBS Volume Attach, Mount & Persistence

### Objective
Understand how persistent storage works in EC2 by attaching an external EBS volume, mounting it inside Linux, and ensuring data survives instance reboot.

This exercise focuses on the difference between **AWS-level attachment** and **OS-level mounting**.

---

## Scenario
An additional EBS volume was attached to a running EC2 instance and made available to the operating system for data storage.

---

## Key Observations

### 1. Attach vs Mount
- Attaching an EBS volume in AWS only makes the disk visible to the instance
- Linux does not automatically mount newly attached disks
- Manual filesystem creation and mounting is required

---

### 2. Disk Detection
- Root volume appeared as `nvme0n1`
- Newly attached EBS volume appeared as `nvme1n1`
- NVMe naming is standard for modern EC2 instance types

---

### 3. Filesystem & Mounting
- The new volume had no filesystem initially
- A filesystem was created before mounting
- The volume was mounted at `/data`
- Data written to the mount point was accessible immediately

---

### 4. Persistence Across Reboot
- By default, mounts do not survive reboot
- `/etc/fstab` was configured using the volume UUID
- The `nofail` option was used to prevent boot failure
- After reboot, the volume remained mounted and data persisted

---

## What Data Persists
- Data stored on EBS volumes survives:
  - Reboot
  - Stop / Start
- Instance store (ephemeral storage) does not persist

---

## Production Relevance
- EBS provides persistent storage independent of EC2 lifecycle
- Correct fstab configuration is critical; incorrect entries can cause boot failures
- Using UUID instead of device name is a production best practice
- This pattern is used for application data, logs, and databases

---

## Key Takeaway
EC2 provides compute, not durability.  
Persistent data must live on EBS and be explicitly managed at the OS level.

- Zero or minimal downtime
- Better fault tolerance
