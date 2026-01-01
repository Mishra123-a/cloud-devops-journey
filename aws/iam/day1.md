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
