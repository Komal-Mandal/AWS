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

# Step-by-step User , Group, Policy creation

## Sign in

- Sign in to the AWS Management Console using an admin account (not the root account). Go to Services → IAM.

- Create a Group 

- In IAM, go to User groups (or Groups) → Create group.

- Give it a name (e.g., Developers).

- Attach permissions: choose one or more AWS Managed policies (e.g., AmazonS3ReadOnlyAccess) or skip and attach later.

- Click Create group.

- Create a User

- In IAM, go to Users → Add users.

- Enter username (e.g., komal).

- Select access type:

- Programmatic access (for CLI/SDK) → creates Access Key ID + Secret Access Key.

- AWS Management Console access → creates a console password.

- You can select both if needed.

- Click Next: Permissions.

- Assign Permissions

- Choose Add user to group and select the group you created (Developers).

- Or attach policies directly to the user .

- Click Next → optionally add tags → Create user.

- Save credentials

- On success, download the .csv or copy the Access Key ID and Secret Access Key shown. Secret key is shown only once — save it securely.

- Enable Console Password Reset (if console access created)

- If you created console access, choose whether you want to Require password reset at first login.

- Enable MFA for the user (important)

- IAM → Users → Select user → Security credentials → Manage MFA device → choose Virtual MFA device.

- Scan QR with an authenticator app (Google Authenticator, Authy), enter two consecutive codes and Assign.

- Test the user

- Ask the user to sign in using the IAM console sign-in URL (account ID or alias) or test with AWS CLI after aws configure.

- Optional: Create customer-managed policy

- IAM → Policies → Create policy → use Visual editor or JSON → Review policy → Create → attach to group/user.

- Cleanup (if needed)

- To remove a user: detach policies, remove from groups, delete access keys, delete login profile, delete user.





