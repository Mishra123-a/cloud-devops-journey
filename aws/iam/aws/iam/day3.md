## IAM Day 3 – S3 Upload & Read Access Without Delete

### Scenario
A developer or application must be able to upload and read files from a single S3 bucket but must not be allowed to delete any objects or access other buckets.

This is required to prevent accidental data loss and enforce least-privilege access.

---

### What I did
- Created a dedicated S3 bucket for testing
- Designed a custom IAM policy allowing:
  - List bucket
  - Upload objects
  - Read objects
- Attached the policy to an IAM user
- Tested permissions using the AWS console

---

### What broke / issues faced
- IAM user could not see any S3 buckets in the console
- Delete operation failed with AccessDenied error

---

### Root cause
- The S3 console requires `s3:ListAllMyBuckets` to display bucket names
- Object-level permissions (`PutObject`, `GetObject`) alone are not enough for console visibility
- `DeleteObject` was never allowed, so IAM implicitly denied delete requests

---

### What I learned
- `s3:ListAllMyBuckets` is required to list buckets in the console
- `s3:ListBucket` controls listing objects inside a specific bucket
- Object actions require object ARNs (`bucket-name/*`)
- IAM follows implicit deny by default
- Absence of permission is enough to block destructive actions

---

