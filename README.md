# AWS-EC2-Setup
Step by Step configuration of an AWS EC2 server for hosting web applications
This repository documents the step by step process of setting up and configuring an AWS EC2 instance to host a web application

## Table of Contents
[Launching an EC2 instance](#launching-an-ec2-instance)
[Mounting The Download Folder of Private Key in Windows 11 on WSL](#mounted-the-download-folder-of-private-key-in-windows11-on-wsl)
[Copied Private Key From Mounted Directory(Windows 11) to Home Directory in Linux Using wsl.exe](#Copied-Private-Key-From-Mounted-Directory-to-Home-Directory-in-Linux)
[Creating a Symlink & Change Private Key Permissions](#Creating-a-Symlink-&-Change-Private-Key-Permissions)
[Connecting via SSH](#connecting-via-ssh)
[Installing Required Software](#installing-required-software)
[Deploying a Web Application](#deploying-a-web-application)
[Securing The Server](#securing-the-server)

## Launching an EC2 instance
Log into the [AWS Console](https://aws.amazon.com/console/)
Navigate to EC2 and click "Launch Instance"
Configure the instance:
  - Amazon Machine Image (AMI) : Amazon Linux 2
  - Instance Type: t2.micro
  - Key Pair: Created an ED25519 key pair
  - Security group: Allow SSH (port 22) and HTTPS (port 443)

![AWS-EC2](https://github.com/user-attachments/assets/3d650385-b2e4-40a3-b5c7-26c179068b66)

## Mounting The Download Folder of Private Key in Windows 11 on WSL
Used the following command to mount the directory from Windows on WSL Ubuntu:
  - mnt/c/users/anuad/Downloads
![mount windows directory](https://github.com/user-attachments/assets/1d269b7e-4f16-42a0-9a68-7c7c6fc8c30a)

## Copying Private Key From Mounted Directory(Windows 11) to Home Directory in Linux Using wsl.exe
Used the folllowing command:
  - wsl.exe -v C:\Users\anuad\Downloads /mnt/~
![copy from win11 to wsl](https://github.com/user-attachments/assets/0ac1c683-58ea-472d-82ec-730acffae608)

## Creating a Symlink & Change Private Key Permissions
Used the following commands to create a symlink between the downloaded private key on host windows 11 to the WSL Ubuntu platform, and to change its permissions:
  - ln -s /mnt/c/Users/anuad
  - sudo chmod 600 FirstServerKey.pem

## Connecting via SSH 
Run the following command to connect to the instance: 
  - ssh -i "FirstServerKey.pem" ec2-user@52.73.66.59
![change permission and connect via ssh](https://github.com/user-attachments/assets/a48b3415-323f-4a54-aa97-e3503f26af9d)

## Installing Required Software
Updated the server and installed Apache using the following commands:
  - sudo yum update -y
  - sudo yum install httpd -y
  - sudo systemctl start httpd
  - sudo systemctl enable httpd
  - ![install apache and update amazon linux server](https://github.com/user-attachments/assets/2b575d6c-3b0b-412c-b91a-ee3ea28812f9)
