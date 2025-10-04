
#  AMI (Amazon Machine Image) 

## 🔹 What is an AMI?

- AMI (Amazon Machine Image) is a template used to launch EC2 instances.

 It includes:

- Operating system (e.g., Ubuntu, Amazon Linux, Windows).

- Software packages (e.g., Nginx, Python, custom apps).

- Configuration (custom scripts, environment settings).

- Think of it like a snapshot + template of an instance.

- When you create an AMI from an EC2, you can launch new EC2s with the exact same setup.

## 🔹 Example Workflow

- Create EC2 with name test.

- Install/configure Nginx.

- Create an AMI from test.

- Launch a new instance test2 using that AMI.

## 1. Create EC2 Instance (test)

- Launch an EC2 instance (Ubuntu)  Name it test.

- Install software (like Nginx, MySQL, your app, etc).

## 2. Create an AMI from EC2

- Go to EC2 Console → Instances → Select instance test.

- Click Actions → Image and templates → Create Image.

- Give it a name, e.g., test-ami.

- AWS will create an AMI (takes a few minutes).

![alt text](image.png)

## 3. Launch New Instance from AMI

- Go to AMIs in EC2 Dashboard.

- Select test-ami.

- Click Launch instance from image.

- Name the new instance test2.

- Now test2 will be an exact clone of test (same OS + software + configuration).

![alt text](<Screenshot 2025-10-04 090658.png>)

![alt text](<Screenshot 2025-10-04 090723.png>)

![alt text](<Screenshot 2025-10-04 090818.png>)



