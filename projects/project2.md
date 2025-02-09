---
layout: default
title: "Chize's Portfolio of Security Projects"
description: "This project involves designing and implementing a network segmentation strategy to enhance both security and performance. By dividing the network into isolated subnets using VLANs, different types of devices and trust zones can be separated, minimizing the risk of unauthorized access and optimizing traffic management."
image: "media/securityportfoliobanner.png"
---

# Deploying a Secure VPN Server on AWS

## Overview
**Title:** Deploying a Secure VPN Server on AWS  
**Objective:** Set up a secure VPN server in AWS to provide encrypted, private access to cloud resources and secure client traffic.

---

## VPN Installation and Configuration

### Description  
Installed and configured OpenVPN Access Server on a AWS EC2 instance.

### Steps  
1. Launch EC2 instance from the AWS Marketplace using the "OpenVPN Access Server" image.
2. Ensure the instance size is **t2.micro** to remain within the free tier.
3. Connect to the instance via SSH using the created private key.

![awsvpnscrn1](media/awsvpn1.png)
![awsvpnscrn1](media/awsvpn2.png)
Here is a screenshot of the EC2 instance being created & the ssh information. {public ip and instance id blocked out for obvious reasons)

Commands Used  
```bash
cd Downloads/
ssh -i X448.pem openvpnas@<public-ip-address>
sudo passwd openvpn
```
![awsvpnscrn1](media/awsvpn3.png)
Here is a screen of SSH sucessfully connected & initial configuration finished.

### Installed Packages  
- OpenVPN Access Server for VPN management and encrypted connectivity.

---

## VPN Server Access and Routing Setup

### Description  
Configured the VPN server for secure traffic routing.

### Steps  
1. Accessed the VPN admin panel at `https://<public-ip>:943/admin`.
2. Logged in using the OpenVPN admin credentials.
3. Enabled full traffic routing through the VPN under **VPN Settings**.
4. Applied and updated server settings.

---

![awsvpnscrn1](media/awsvpn4.png)
Here is a screen showing firefox telling me that this is a self signed certificate. (normally you wouldn't proceed if you aren't setting something up lol)

![awsvpnscrn1](media/awsvpn5.png)
Here is a screen in the OpenVPN admin panel.

---

## EC2 Security Settings

### Description  
Configured security groups to restrict access to trusted IP ranges and set up essential ports for OpenVPN and secure remote administration.

### Steps Taken  
1. **Security Group Configuration**:
   - Restricted inbound rules for SSH (port 22) and OpenVPN (ports 943 and 945) to trusted IP ranges.
   - Allowed public access only to HTTPS (port 443) for secure web services.

2. **Security Group Rules**:
   ```text
   Port     Protocol   Source
   22       TCP        <trusted-ip>/32
   943      TCP        <trusted-ip>/32
   945      TCP        <trusted-ip>/32
   443      TCP        0.0.0.0/0
   ```

### Security Enhancements  
- Reduced the risk of unauthorized access by restricting administrative ports to trusted IP addresses.
- Hardened VPN and web service access by securing sensitive ports.

---

## Elastic IP Configuration

### Description  
Assigned a static Elastic IP to the EC2 instance running the OpenVPN server to maintain a consistent IP address across restarts.

### Steps Taken  
1. Created an Elastic IP in the EC2 console.
2. Associated the Elastic IP with the running EC2 instance.

### Security Enhancements  
- Ensured stable client connectivity by preventing IP changes on server restarts.
- Reduced the risk of configuration errors with consistent IP address usage in OpenVPN.

---

## OpenVPN User Permissions

### Description  
Created an admin and user group, changed passwords for both admin and user accounts.

### Steps Taken  
1. Created an **admin group** and added administrative accounts in the OpenVPN Admin Panel.
2. Created a **user group** and added standard VPN user accounts.
3. Changed the passwords for both admin and user accounts for enhanced security.

### Security Enhancements  
- Improved security by organizing users into groups and enforcing password changes.
- Reduced risk by limiting user access and updating connection profiles with a static IP.

---



## Client Connection Setup

### Description  
Set up client devices to connect to the VPN server.

### Steps  
1. Navigated to the user portal at `https://<public-ip>:943`.
2. Downloaded and sent the OpenVPN client with embedded profile to two of my friends to test it out.

---

## Testing and Validation

### Description  
Verified VPN connectivity and security on friends devices.

### Steps  
1. Tested connection by logging in from a remote device.
2. Checked IP address to confirm traffic was routed through the VPN.


---

## Challenges and Solutions

### Challenge 1: SSH server still prompting for a password  
**Solution:**  
Verified that `PasswordAuthentication` was set to `no` and restarted the SSH service.

### Challenge 2: Public key authentication failed  
**Solution:**  
Checked key permissions (700 for `.ssh`, 600 for `authorized_keys`) and ownership.

### Challenge 3: Configuration files causing conflicts  
**Solution:**  
Reviewed additional configuration files in `/etc/ssh/sshd_config.d/` for overrides.

---

## Reflection and Future Improvements

### Reflection  
This project enhanced my knowledge of AWS, system security, and VPN infrastructure.

### Future Improvements  
- Automate VPN setup using infrastructure-as-code (IaC) tools like Terraform.
- Implement IP allowlists and advanced traffic filtering.
- Enable MFA for additional security.
- Configure monitoring and alerts for VPN server events.

---

## Conclusion

This project successfully deployed and secured a VPN server on AWS, enabling encrypted access to cloud resources and enhancing system security through best practices.
