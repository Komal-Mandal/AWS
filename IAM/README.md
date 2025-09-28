## 🌐 AWS IAM (Identity and Access Management)

### 🔹 1. What is IAM?

IAM (Identity and Access Management) is a global AWS service used to securely control access to AWS resources.

### It manages:

- Users (who can log in)

- Groups (collections of users)

- Roles (temporary permissions)

- Policies (rules that define what is allowed/denied)

- Think of IAM as the security guard of AWS.

### 🔹 2. Key Features of IAM

- Free service (no extra cost).

- Granular permissions – Allow or deny specific actions.

- Shared access – Multiple users can access AWS securely.

- Multi-Factor Authentication (MFA) for extra security.

- Temporary credentials via IAM roles.

- Global service – Works across all AWS regions.

- Integration with AWS services (EC2, S3, RDS, Lambda, etc.).

### 🔹 3. Core Components of IAM

### 👤 IAM Users

- Represents a person or application.

- Each user has:

- Username + Password (for AWS console)

- Access keys (for CLI/SDK)

### 👥 IAM Groups

- A collection of IAM users.

- Permissions are attached to the group, not individually.

- Example:

- Group: Developers → Permissions: EC2, S3

- All users in Developers inherit the same access.

### 🎭 IAM Roles

- Used for temporary access to AWS resources.

- No username/password – instead, users/services assume roles.

- Example:

- EC2 instance assumes a role → Can access S3 bucket without storing credentials.

###  IAM Policies

- JSON documents that define permissions.

- Example policy:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket"],
      "Resource": ["arn:aws:s3:::mybucket"]
    }
  ]
}
```

- Effect: Allow/Deny

- Action: What the user can do

- Resource: Where they can do it

### 🔹 4. Types of Policies

- AWS Managed Policies – Predefined by AWS (e.g., AmazonS3FullAccess).

- Customer Managed Policies – Created by you.

### 🔹 5. Authentication & Authorization

- Authentication = Verifying who you are (username, password, MFA).

- Authorization = Verifying what you can do (policies).







