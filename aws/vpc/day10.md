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

Meaning:
- All subnets inside the VPC can communicate internally
- This route cannot be removed

---

## 3) How Subnet Association Works
A subnet must be associated with exactly one route table:
- If you don’t associate a custom route table, it uses the **main route table**
- Route tables apply at the **subnet level**, not instance level

Key rule:
> **Subnet routing behavior depends on the route table attached to that subnet.**

---

## 4) What Makes a Subnet Public vs Private

### Public Subnet (Definition)
A subnet is **public** only if its route table has: 0.0.0.0/0 → Internet Gateway (IGW)
