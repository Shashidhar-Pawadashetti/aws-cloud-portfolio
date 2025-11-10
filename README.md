# Shashidhar's AWS Cloud Engineering Portfolio

Hello! I'm a Computer Science student currently on a journey to become an **AWS Certified Solutions Architect**. This repository serves as a living portfolio of all the hands-on projects, labs, and architecture patterns I am learning and building.

You can follow my professional journey and day-to-day takeaways on [LinkedIn](https://www.linkedin.com/in/shashidhar-pawadashetti-a58461280/).

---

## Table of Contents

### Project 0: Securing My AWS Account with IAM

* **Objective:** To establish a secure baseline for my AWS account by moving away from the root user and enforcing best practices for access control.
* **Services Used:**
    * `AWS Identity and Access Management (IAM)`: To create users, groups, and policies.
* **What I Did:**
    1.  **Stopped using the Root user** for daily tasks.
    2.  Created a new **IAM Administrator User** for myself with full admin privileges.
    3.  Created a **`developers` Group** and a **`billing` Group** with limited, permission-specific policies.
    4.  Set up a **custom password policy** to enforce strong passwords for all new users.
    5.  Enabled **Multi-Factor Authentication (MFA)** on my Root user account and on my new Administrator account.
* **What I Learned:**
    * The "Principle of Least Privilege" (the most important concept in IAM): Only give users the *exact permissions* they need to do their job, and nothing more.
    * Why you should **never** use the Root user for anything other than billing or initial account setup.
    * How Groups make it easy to manage permissions for many users at once.
    * That MFA is the single most effective way to protect an account from being compromised, even if the password is stolen.

---

* [Project 1: Static Website Hosting on S3](#project-1-static-website-hosting-on-s3)
* [Project 2: 3-Tier Web Application VPC](#project-2-3-tier-web-application-vpc)
* [More Projects Coming Soon...](#)

---

## AWS Projects

### Project 1: Launching a Secure EC2 Virtual Server

* **Objective:** To launch a "virtual server" (EC2 Instance) in the AWS cloud and establish a secure remote connection to it from my Windows machine.
* **Services Used:**
    * `Amazon EC2 (Elastic Compute Cloud)`: To provision the virtual server (a `t2.micro` instance on Amazon Linux).
    * `EC2 Key Pair`: To create a `.pem` file used to securely authenticate my SSH connection.
    * `Security Groups`: To act as a virtual firewall for the instance.
* **What I Did:**
    1.  Launched a free-tier eligible `t2.micro` EC2 instance.
    2.  Created a new Key Pair and securely downloaded the `.pem` file.
    3.  Configured the instance's **Security Group** to allow **SSH (port 22)** traffic *only* from my personal IP address. (This is a critical security step!)
    4.  Used **OpenSSH** (which is built into Windows Terminal/PowerShell) to connect to my instance using the `ssh` command.
* **What I Learned:**
    * EC2 is the core "Infrastructure as a Service" (IaaS) offering from AWS.
    * A Security Group acts as a *stateful firewall* for an instance. By default, it blocks all incoming traffic, and you must explicitly "allow" ports.
    * A Key Pair is the secure way to "log in" to a Linux server, replacing a traditional password.
    * Modern Windows (10/11) no longer requires PuTTY for SSH, making the `ssh -i "key.pem" ec2-user@<ip-address>` command a fast and standard way to connect.

---

### Project 2: Launching a Secure EC2 Virtual Server

* **Objective:** To launch a "virtual server" (EC2 Instance) in the AWS cloud and establish a secure remote connection to it from my Windows machine.
* **Services Used:**
    * `Amazon EC2 (Elastic Compute Cloud)`: To provision the virtual server (a `t2.micro` instance on Amazon Linux).
    * `EC2 Key Pair`: To create a `.pem` file used to securely authenticate my SSH connection.
    * `Security Groups`: To act as a virtual firewall for the instance.
* **What I Did:**
    1.  Launched a free-tier eligible `t2.micro` EC2 instance.
    2.  Created a new Key Pair and securely downloaded the `.pem` file.
    3.  Configured the instance's **Security Group** to allow **SSH (port 22)** traffic *only* from my personal IP address. (This is a critical security step!)
    4.  Used **OpenSSH** (which is built into Windows Terminal/PowerShell) to connect to my instance using the `ssh` command.
* **What I Learned:**
    * EC2 is the core "Infrastructure as a Service" (IaaS) offering from AWS.
    * A Security Group acts as a *stateful firewall* for an instance. By default, it blocks all incoming traffic, and you must explicitly "allow" ports.
    * A Key Pair is the secure way to "log in" to a Linux server, replacing a traditional password.
    * Modern Windows (10/11) no longer requires PuTTY for SSH, making the `ssh -i "key.pem" ec2-user@<ip-address>` command a fast and standard way to connect.

---

### Project 2: 3-Tier Web Application VPC

* **Objective:** To design and build a foundational, secure, and scalable network infrastructure in AWS to host a classic 3-tier application (Web, App, Database).
* **Services Used:**
    * `Amazon VPC`: To create a logically isolated virtual network.
    * `Subnets`: Created public subnets for web-facing resources (like load balancers) and private subnets for internal resources (like application servers and databases).
    * `Route Tables`: Configured routing for public subnets (via an Internet Gateway) and private subnets (via a NAT Gateway).
    * `Security Groups`: Acted as a stateful firewall for EC2 instances.
    * `NACLs`: Acted as a stateless firewall for the subnets.
* **Architecture Diagram:**
    * (Coming Soon - *This is a great one to draw and upload!*)
* **What I Learned:**
    * The critical importance of a "defense in depth" security model.
    * How to control inbound and outbound traffic using Security Groups (for instances) and NACLs (for subnets).
    * The difference between a public and private subnet and why it's the most important concept in cloud security.
    * The role of a NAT Gateway in allowing instances in private subnets to access the internet for updates without being exposed to incoming traffic.

---
