
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

<img width="1508" height="404" alt="Screenshot 2025-10-04 090048" src="https://github.com/user-attachments/assets/ac471041-6474-4603-81ac-ef34f3c2eddb" />


## 3. Launch New Instance from AMI

- Go to AMIs in EC2 Dashboard.

- Select test-ami.

- Click Launch instance from image.

- Name the new instance test2.

- Now test2 will be an exact clone of test (same OS + software + configuration).

<img width="1527" height="303" alt="Screenshot 2025-10-04 090658" src="https://github.com/user-attachments/assets/c64fbb0b-f154-4c8d-a1d0-23446c56ec57" />

<img width="1260" height="356" alt="Screenshot 2025-10-04 090723" src="https://github.com/user-attachments/assets/ad236711-7b25-4e34-9f2a-a9530898a355" />

<img width="1501" height="362" alt="Screenshot 2025-10-04 090818" src="https://github.com/user-attachments/assets/95bed75b-9aa0-476f-9eba-968685540b61" />







