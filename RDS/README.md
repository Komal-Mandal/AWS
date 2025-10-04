
# 📘 Deploying a Dynamic Website Using EC2 + Docker + Amazon RDS

## 🔹 What is Amazon RDS?

Amazon RDS (Relational Database Service) is a managed relational database service that lets you run databases in the cloud without worrying about server management, backups, or patching.

### Key Features:

- Supports MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Aurora.

- Automated backups, snapshots, and high availability.

- Multi-AZ deployment for failover.

- Read replicas for scaling reads.

- Secure (VPC, IAM, encryption).

## 🔹 Why Use RDS?

- No need to manage database servers manually.

- High availability and automatic failover.

- Easy to scale storage and compute resources.

- Secure and compliant with encryption.

- Ideal for dynamic web applications that need a database backend.

## step 1: Create an RDS Instance

- Go to AWS Console → RDS → Create Database.

- Select MySQL (or your preferred engine).

- Enter DB details:

- DB Identifier: mydb-instance

- Master Username: admin

- Password: abcd1234

- DB instance size: db.t3.micro (free tier eligible)

#### Connectivity:

- Public access: Yes (for testing) or No (if using EC2 in same VPC)

- VPC Security Group: Allow inbound MySQL (port 3306) from your EC2 instance.

- Click Create Database.

- Note the endpoint.

## Step 2: Launch EC2 Instance for Website

- Go to EC2 → Launch Instance.

- Select Amazon Linux 2 or Ubuntu 22.04.

- Instance type: t2.micro (free tier)

- Key Pair: Use an existing key or create a new one.

- Security Group:

- Inbound: HTTP 80, SSH 22

- Outbound: all traffic

- Launch instance and note public IP.

## Step 3: Install Docker on EC2

```
sudo yum install -y docker

sudo service docker start

sudo usermod -aG docker ec2-user

sudo docker pull philippaul/node-mysql-app:02

```
## Step 4: Run Docker Container Connecting to RDS
```
sudo

docker run --rm -p 80:3000 

-e DB_HOST="your-db-hostname" 

-e DB_USER="your-db-username" 

-e DB_PASSWORD="your-db-password" 

-d philippaul/node-mysql-app:02

```

## Step 5: Configure Security Groups

- EC2 Security Group: Allow HTTP (80) for users

- RDS Security Group: Allow MySQL (3306) from EC2 Security Group

## step 6: Access Your Website

- Find your EC2 Public IP

- Go to AWS Console → EC2 → Instances

- Look for Public IPv4 of your EC2 instance

- Open your browser

- Paste the public IP 

#### Result

- The Node.js app running in Docker should load

- Any dynamic content that requires the database (RDS) should work automatically

#### Important Notes

- If it doesn’t load:

- Check EC2 Security Group allows HTTP (port 80) inbound from 0.0.0.0/0.

- Ensure your Docker container is running: