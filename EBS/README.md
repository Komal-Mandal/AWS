
# Amazon Elastic Block Store (EBS)

## 🔹 What is EBS?

- Amazon Elastic Block Store (EBS) is a block-level storage service designed for use with EC2 instances.
It works like a virtual hard disk in the cloud:

- You can attach it to your EC2 instance.

- Data persists even after stopping the instance.

- You can take snapshots (backups) and restore anytime.

- Think of EBS as the hard drive of your cloud virtual machine.

## 🔹 Key Features

- Persistent, durable storage (survives instance stop/start).

- Flexible – resize volumes without downtime.

- Multiple types (SSD & HDD) for different use cases.

- Snapshots for backup and disaster recovery.

- Encryption at rest and in transit.

- High performance for databases and critical workloads.

## 📘 AWS Workflow: EC2 + EBS + Snapshot + New Volume

This guide explains how to:

- Create an EC2 instance

- Create an EBS volume and attach it

- Create a Snapshot of the volume

- Create a new volume from the snapshot

- Attach the new volume back to the EC2 instance

## 🔹 1. Launch an EC2 Instance

- Go to AWS Console → EC2 → Launch Instance.

- Select an AMI (Amazon Linux 2, Ubuntu, etc.).

- Choose instance type (t2.micro for free tier).

- Configure VPC, subnet, and Security Group.

- Add storage (default root volume).

- Create/choose key pair → Launch.

- Now your EC2 is ready.

##🔹 2. Create & Attach an EBS Volume

- Go to EC2 → Volumes → Create Volume.

- Size: e.g., 10GB.

- Type: gp3 (general purpose).

- Availability Zone: must match your EC2 instance’s AZ.

- After creation → Actions → Attach Volume.

- Choose your EC2 → attach as /dev/sdf.

## 🔹 3. Create a Snapshot of EBS

- Go to EC2 → Volumes → Select volume → Actions → Create Snapshot.

- Enter description (e.g., “Backup of Data Volume”).

- Snapshot will appear under Snapshots.

##🔹 4. Create New Volume from Snapshot

- Go to EC2 → Snapshots → Select Snapshot → Actions → Create Volume.

- Choose:

- Size (can be equal or larger).

- Same AZ as EC2.

- Create the volume.

##🔹 5. Attach the New Volume to EC2

- Go to EC2 → Volumes → Select New Volume → Actions → Attach Volume.

- Attach to the same EC2 instance (e.g., /dev/sdg).

## 6. Mount the New Volume

- on EC2

```
# Check again
lsblk

# Create mount directory
sudo mkdir /backup

# Mount the new volume
sudo mount /dev/xvdg /backup

# Verify files (it should have same data as original volume)
ls /backup
```
## Now you have two volumes on your EC2:

- /data → original EBS

- /backup → new volume from snapshot (copy).

## 🔹 Why We Use EBS with EC2

### What Happens When EC2 is Terminated 

## 1. root volume

When you launch an EC2 instance, it comes with a root volume (the OS disk).

By default, the root volume has the setting “Delete on Termination = true”.

This means:

If you terminate the EC2 instance, the root volume is automatically deleted.

Data on the root volume is lost permanently unless you change this setting before termination.

## 2. EBS Volumes (Additional Volumes)

If you create additional EBS volumes (not root), they are persistent by default.

Even if the EC2 instance is terminated, the EBS volume still exists.

You can attach it to a new EC2 instance later.

