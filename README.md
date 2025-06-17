# EC2-Ansible-git
To set up an EC2 web server that loads an index.html file from a Git repository, you can follow the steps below. This walkthrough assumes you're using Amazon Linux 2 and a public GitHub repo.

STEPS: LAUNCH A LINUX EC2 INSTANCE
1.Log in to AWS Console.

2.There you need to search EC2.This the dashboard for EC2,to create an instance you need to click on Launch Instance.

3.Name your instance,Then in the Application and OS Images, you have to select an Operating system.Here, you are going to select  as your Operating system.8.For Amazon Machine Image (AMI), select the latest AMI that is available. In this case it is ubuntu server 22.02 LTS.

4.Keep architecture to default as 64-bit (x86)

5.Now you must choose an instance type. There are more instance types with higher specifications available, but for the time being, you must select t2.micro. This instance type is qualified for the free tier.

6.In the key pair, you have to create a key pair, so that you can log in to your virtual machine. click on create new key pair. First you have to name your keypair.Then select the key pair type as RSA.For the private key file format, select .pem,Now click on create key pair,a file would have been downloaded automatically

7.If you will take a look at network settings, you will see a VPC which is required and it is a default VPC,The subnet has no preference because you haven’t given it any.

8.The auto assign public IP feature is enabled.
9.In the firewall option, you will see that it is creating a new security group, you can change its name and description, but for the time being keep it to default.

10.And the security group you will see this Inbound security group rules. These Inbound rules are used for virtual machine to log in to different areas of interest. Let it be default too.
   Allow http and https access
   
11. In the user data section You write a script that:
    Installs Ansible on the EC2 instance
    Pulls an Ansible playbook from GitHub
    Runs it locally on the same EC2 instance
    
   #!/bin/bash
# Update OS and install Ansible
apt update -y
apt install -y ansible git

# Switch to home directory
cd /home/ubuntu

# Clone your Git repo with playbook
git clone https://github.com/sharda-Ekbote/EC2-Ansible-git.git

# Go to playbook directory
cd EC2-Ansible-git

# Run the playbook locally on the EC2
ansible-playbook -i localhost, -c local playbook.yml
