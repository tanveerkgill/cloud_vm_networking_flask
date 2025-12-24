# Flask App Deployment on a Cloud VM (AHI 504 – Assignment 2)

## Student Information
**Name:** Tanveer Kaur  
**Cloud Provider:** Google Cloud Platform (GCP)  
**VM Name:** flask-5003  

## Video Walkthrough
**Zoom / Loom Recording:** PASTE YOUR VIDEO LINK HERE  

---

## Project Overview
This assignment demonstrates how to deploy a simple Flask web application on a Google Cloud virtual machine and expose it to the public internet using custom firewall rules. The project builds on VM lifecycle concepts and introduces networking configuration, Linux environment setup, and application hosting.

The Flask application is publicly accessible at:

👉 **http://35.224.118.110:5003**

---

## Step-by-Step Implementation

## 1. Virtual Machine Creation
I created a virtual machine using Google Compute Engine.

- Navigated to **Compute Engine → VM instances → Create instance**
- Named the VM **`flask-5003`**
- Selected **Ubuntu 22.04 LTS** as the operating system
- Chose the **e2-micro** machine type to remain within free-tier limits
- Confirmed that an **External IP address** was assigned
- Created the VM and waited for provisioning to complete

📸 **VM Instance Created**
  
<img width="1158" height="762" alt="VM Creation" src="https://github.com/user-attachments/assets/cabf7e67-b97d-41a8-b4aa-4fabf7aa3e2b" />

---

## 2. Networking Configuration (Port 5003)
To allow external access to the Flask app, I created a firewall rule allowing inbound TCP traffic on port **5003**.

- Navigated to **VPC network → Firewall → Create firewall rule**
- Configured the rule as follows:
  - **Name:** allow-tcp-5003
  - **Direction:** Ingress
  - **Action:** Allow
  - **Targets:** All instances in the network
  - **Source IPv4 ranges:** `0.0.0.0/0`
  - **Protocols and ports:** `tcp:5003`
- Saved the firewall rule and confirmed it was active

📸 **Firewall Rule Allowing Port 5003**
  
<img width="1267" height="738" alt="Firewall Rule" src="https://github.com/user-attachments/assets/dc6f4845-33ae-4cf6-a17c-235cca7e59dd" />

---

## 3. OS Update and Environment Setup
After launching the VM, I connected using SSH from the Google Cloud Console.

### Update system packages
```bash
sudo apt update && sudo apt upgrade -y
