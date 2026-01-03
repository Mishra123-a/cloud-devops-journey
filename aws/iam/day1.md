## IAM Day 1 – Users, Groups, ReadOnly Policy

### What I did
- Created IAM user
- Tested ReadOnly EC2 access
- Compared user vs group permissions

### What broke
- Launch instance permission denied (expected)

### What I learned
- ReadOnly policy allows describe actions only
- Groups are better than attaching policies directly to users

  
## IAM Day 2 – Custom Policy, Region Issue, Operator Access
What I did
Created custom IAM policy for EC2 start/stop
Attached policy to ec2-operators group
Tested permissions using IAM user
## What broke
Instance was not visible initially
Root user was in eu-north-1, IAM user in us-east-1
## What I learned
EC2 instances are region-scoped
IAM controls actions, not resource ownership
Start/Stop permissions do not allow launch or terminate
