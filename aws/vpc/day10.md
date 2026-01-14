### Objective
Understand how AWS routing works inside a VPC and why **subnets become public/private based on route tables**, not naming.

---

## 1) What a Route Table Really Is
A route table is a set of rules that decides:
> **Where traffic should go next based on destination CIDR.**

Route tables do **not** allow/deny traffic.  
They only provide the **next hop**.

Security is handled by:
- Security Groups (stateful)
- Network ACLs (stateless)

---

## 2) The "local" Route (Most Important Default)
Every VPC route table automatically contains:

- Destination: **VPC CIDR**
- Target: **local**

Example: ### Objective
Understand how AWS routing works inside a VPC and why **subnets become public/private based on route tables**, not naming.

---

## 1) What a Route Table Really Is
A route table is a set of rules that decides:
> **Where traffic should go next based on destination CIDR.**

Route tables do **not** allow/deny traffic.  
They only provide the **next hop**.

Security is handled by:
- Security Groups (stateful)
- Network ACLs (stateless)

---

## 2) The "local" Route (Most Important Default)
Every VPC route table automatically contains:

- Destination: **VPC CIDR**
- Target: **local**

Example: 10.0.0.0/18 → local
