## IAM Day 3 – Explicit Deny to Protect Production

### Scenario
Production EC2 instances must not be terminated accidentally, even by users with high privileges.

### What I did
- Attached AmazonEC2FullAccess to an IAM user
- Created a custom IAM policy with explicit DENY for ec2:TerminateInstances
- Attached both policies to the same user

### What broke / surprised me
- Even with EC2 Full Access, terminate action was blocked

### What I learned
- IAM evaluates all policies together
- Explicit DENY always overrides ALLOW
- This pattern is used to protect production resources.
