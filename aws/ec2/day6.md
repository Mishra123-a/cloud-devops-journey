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
- Zero or minimal downtime
- Better fault tolerance
