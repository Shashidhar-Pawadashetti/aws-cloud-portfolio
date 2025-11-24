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
### Project 3: EC2 Advanced Design Patterns

* **Objective:** To move beyond a single instance and learn to design EC2 solutions optimized for specific workloads (high availability, high performance, or cost-efficiency).
* **Services/Features Studied:**
    * `EC2 IP Addressing`: Public, Private, and Elastic IPs
    * `EC2 Placement Groups`: Cluster, Spread, and Partition
    * `Elastic Network Interfaces (ENI)`
    * `EC2 Hibernate`
* **What I Learned (Key Architectural Takeaways):**
    * **IP Addressing:** I learned the *purpose* of each IP type. A **Public IP** is temporary and fine for testing. A **Private IP** is for internal communication (e.g., your app server talking to your database). An **Elastic IP** is essential for production, giving your server a permanent, static public address that you can re-map if an instance fails.
    * **Placement Groups (Performance vs. Availability):** This was a major "aha!" moment.
        * **Spread Group:** I used this to deploy instances on different physical hardware. This is the **best choice for high availability** for a critical application.
        * **Cluster Group:** I used this to co-locate instances in the same rack for extremely low-latency, high-throughput communication. This is ideal for **High-Performance Computing (HPC)**.
    * **Elastic Network Interface (ENI):** I learned an ENI is a virtual network card. The key feature is that you can **detach it from a failed instance and re-attach it to a new one**, allowing you to transfer its private IP, elastic IP, and MAC address. This is a powerful tool for building failover solutions.
    * **EC2 Hibernate:** I practiced hibernating an instance. This saves the contents of the instance's RAM to the EBS root volume, allowing for a much faster "boot-up" than a full restart. This is a great **cost-saving and efficiency tool** for applications that take a long time to initialize.

---

### Project 3: Managing Persistent Storage with EBS

* **Objective:** To understand how to manage data persistence in AWS using Elastic Block Store (EBS) and protect data using Snapshots.
* **Services Studied:**
    * `Amazon EBS (Elastic Block Store)`: Network-attached, persistent block storage.
    * `EBS Snapshots`: Point-in-time backups.
    * `Instance Store`: Ephemeral, physically attached storage (Theory).
* **What I Did:**
    1.  **Created a new EBS Volume** (General Purpose gp3) in the same Availability Zone as my EC2 instance.
    2.  **Attached the Volume** to the running instance on the fly.
    3.  **Created a Snapshot** of the volume to create a backup.
    4.  **Restored a Snapshot:** I simulated a disaster recovery scenario by creating a *new* volume from that snapshot.
* **What I Learned:**
    * **The "Network Drive" Concept:** EBS is like a USB stick plugged in over the network. It allows data to persist even if the EC2 instance is stopped or terminated (unlike Instance Store, where data is lost if the instance stops).
    * **Availability Zone Lock:** This was a key learning—an EBS volume is **locked** to a specific Availability Zone (e.g., `us-east-1a`). You cannot attach a volume in `1a` to an instance in `1b` directly.
    * **Snapshot Utility:** To move a volume to a different AZ, you must take a Snapshot, and then create a new volume from that Snapshot in the target AZ.
    * **Incremental Backups:** EBS Snapshots are "incremental"—meaning the second snapshot only saves the data that changed since the first one, which saves storage costs.

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
