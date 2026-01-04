## IAM Day 4 – IAM Roles (Service Role vs Human Role, Switch Role, Temporary Access)

### Scenario
Understand IAM Roles deeply by practicing both:
- Service roles (used by AWS services like EC2)
- Human-assumable roles (Switch Role)

Goal was to clearly understand:
- What a role actually is
- Why roles are temporary
- Difference between EC2 roles and human roles
- Why policies are not attached to users for temporary access

---

### What I did
- Created an IAM role with trusted entity as EC2 (service role)
- Attached AmazonEC2FullAccess to the role
- Tried to switch role as IAM user (failed)
- Learned that EC2 service roles cannot be assumed by humans
- Created a separate IAM role with trusted entity as AWS account (human role)
- Logged in as IAM user and successfully switched role
- Tested EC2 access using the role
- Exited the role and observed permissions removed
- Re-assumed the same role again without reattaching any policy

---

### What broke / confusion faced
- Tried to use an EC2 service role for Switch Role
- Pasted trust policy JSON in permission policy editor (got errors)
- Thought role must be created using IAM user instead of root/admin
- Thought temporary role means one-time usage
- Thought policies must be reattached after session expiry
- Access denied appeared for account-level settings and caused confusion

---

### Root cause (understanding gained)
- IAM roles are NOT users; they are temporary permission containers
- Trust policy defines WHO can assume the role
- Permission policy defines WHAT the role can do
- EC2 service roles trust `ec2.amazonaws.com` and cannot be used by humans
- Human-assumable roles trust AWS account and work with Switch Role
- Temporary means time-limited session, not one-time usage
- Policies remain attached to roles; only sessions expire

---

### What I learned (key takeaways)
- IAM users are permanent identities
- IAM roles are temporary responsibilities
- Services and humans use roles differently
- Switch Role creates a temporary session using STS
- Exiting role immediately removes elevated access
- After session expiry, role must be re-assumed, not reconfigured
- Roles are configured once, sessions are created many times

--
