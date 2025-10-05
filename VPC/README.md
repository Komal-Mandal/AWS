
# 🧠 What is a VPC?

A VPC (Virtual Private Cloud) is like your own private network inside AWS Cloud.
Just like you have a Wi-Fi network at home where your devices are connected privately —
a VPC is a private network for your AWS resources like EC2, RDS, Lambda, etc.

You can control everything — IP range, subnets, routing, firewall rules, etc.

#### A VPC is a logically isolated section of the AWS cloud where you can launch AWS resources.
You have full control over:

- IP address ranges

- Subnets (public/private)

- Route tables

- Internet connectivity

- Security (via NACLs and Security Groups)

## 🌍 Structure of a VPC

### 1. CIDR Block (IP Range)

When you create a VPC, you assign an IP address range using CIDR notation.

Example:
```
10.0.0.0/16
```
- means you can have IPs from 10.0.0.0 to 10.0.255.255.

- You can divide this range into subnets later.

### 2. Subnets

- Subnets are smaller networks inside your VPC.

- You divide your VPC CIDR block into subnets for organization.

Example:

```
VPC: 10.0.0.0/16
  ├── Public Subnet: 10.0.1.0/24  
  └── Private Subnet: 10.0.2.0/24  
```
- Public Subnet: Can access the internet (via Internet Gateway)

- Private Subnet: No direct internet access (used for backend DBs, etc.)

### 3. Route Tables

- Control how traffic flows inside your VPC.

- Every subnet must be associated with a route table.

### 4. Internet Gateway (IGW)

- A gateway that connects your VPC to the Internet.

- Must be attached to VPC and route added in route table.

- 📶 Without IGW → Your VPC is private (no internet access).

- 📶 With IGW → Public subnets can reach the Internet.

### 5. NAT Gateway (Network Address Translation)

- Allows private subnets to access the Internet, but not be accessed from the Internet.

- Example: A private EC2 instance downloading updates or connecting to S3.

### 6. Security Groups (SG)

- Work like a firewall for EC2 instances.

- They control inbound and outbound traffic at the instance level.

- Stateful – if you allow inbound traffic, return traffic is automatically allowed.

### 7. Network ACL (NACL)

- Works like a firewall for subnets.

- Stateless – you must allow both inbound and outbound explicitly.

- You can block specific IPs or ports.

# 🪜 Step-by-Step Setup

### Step 1: Create a VPC

- Go to the VPC Dashboard in the AWS Management Console.

- Click Your VPCs → Create VPC.

- Select VPC only.

- Fill in the details:

- Name tag: MyVPC

- IPv4 CIDR block: 10.0.0.0/16

- IPv6 CIDR block: No IPv6 CIDR block

- Tenancy: Default

- Click Create VPC.

#### ✅ Your VPC is now created.

### Step 2: Create Subnets

- We’ll create one public and one private subnet.

- Go to Subnets → Create subnet.

- Select VPC: MyVPC.

- Add the following subnets:

| Name           | IPv4 CIDR Block | Availability Zone | Type    |
| -------------- | --------------- | ----------------- | ------- |
| PublicSubnet1  | 10.0.1.0/24     | ap-south-1a       | Public  |
| PrivateSubnet1 | 10.0.2.0/24     | ap-south-1a       | Private |

- Click Create subnet.

- Two subnets are created.

### Step 3: Create and Attach Internet Gateway (IGW)

- Go to Internet Gateways → Create Internet Gateway.

- Name it: MyIGW.

- Click Create Internet Gateway.

- Select your IGW → Actions → Attach to VPC → select MyVPC → Attach.

- The Internet Gateway is now connected to your VPC.

### Step 4: Create Route Tables
🗺️ Create Public Route Table

- Go to Route Tables → Create route table.

- Name it: PublicRouteTable.

- Select VPC: MyVPC.

- Click Create route table.

- ➕ Add Routes

- Select your PublicRouteTable.

- Go to Routes → Edit routes → Add route:

- Destination: 0.0.0.0/0

- Target: Select your Internet Gateway (MyIGW)

- Save changes.

#### 🔗 Associate Subnet

- Go to Subnet Associations → Edit subnet associations.

- Select your PublicSubnet1.

- Save associations.

- ✅ Public subnet now has internet access.

### Step 5: Create Network ACL (NACL)

- Go to Network ACLs → Create Network ACL.

- Name: MyNACL.

- Select VPC: MyVPC.

- Click Create NACL.

- Go to Subnet associations → Edit subnet associations → select PublicSubnet1.

#### ⚙️ Configure Inbound Rules

| Rule # | Type        | Protocol | Port Range | Source    | Allow/Deny |
| ------ | ----------- | -------- | ---------- | --------- | ---------- |
| 100    | HTTP        | TCP      | 80         | 0.0.0.0/0 | ALLOW      |
| 110    | HTTPS       | TCP      | 443        | 0.0.0.0/0 | ALLOW      |
| 120    | SSH         | TCP      | 22         | Your IP   | ALLOW      |
| *      | All Traffic | All      | All        | 0.0.0.0/0 | DENY       |

#### ⚙️ Configure Outbound Rules

| Rule # | Type        | Protocol | Port Range | Destination | Allow/Deny |
| ------ | ----------- | -------- | ---------- | ----------- | ---------- |
| 100    | All Traffic | All      | All        | 0.0.0.0/0   | ALLOW      |

- ✅ Your public subnet is now protected with a NACL.

## 🚀 Launch an EC2 Instance in Your Custom VPC

### 🪜 Steps 

### Step 1: Open EC2 Dashboard

- Go to AWS Console → EC2 → Launch Instance.

### Step 2: Choose AMI and Instance Type

- Select an OS like Amazon Linux 2 or Ubuntu.

- Choose t2.micro (free tier).

- Step 3: Configure Network (Attach Your VPC)

- In the Network Settings section:

- VPC: Select your custom VPC (e.g., MyVPC).

- Subnet: Choose the public subnet inside that VPC.

- Auto-assign Public IP: ✅ Enable it (to access from internet).

- Security Group: Create or select one that allows:

- SSH (port 22) → for Linux

- HTTP (port 80) → for web access

### Step 4: Storage

- Keep the default 8 GB EBS volume (you can change later).

### Step 5: Key Pair

- Select or create a key pair (.pem) file for SSH login.

### Step 6: Launch the Instance

- Click Launch Instance.

- Your EC2 will now be inside your custom VPC.

### Step 7: Verify VPC Attachment

- Go to:

- EC2 → Instances → Select Your Instance → Networking Tab

- Check:

- VPC ID → should match your own VPC ID

- Subnet ID → should belong to your VPC

- ✅ This confirms that the EC2 instance is attached to your custom VPC.
