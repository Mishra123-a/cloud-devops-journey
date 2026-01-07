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

