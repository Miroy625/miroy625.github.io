# Hardening a Base Ubuntu System

This project involves securing an Ubuntu virtual machine by applying system updates, configuring packages, managing users, and locking down remote access through SSH. Below are the documented steps and tasks performed.

---

## Project Overview

**Title:** Hardening a Base Ubuntu System  

**Objective:** Configure and secure an Ubuntu system by applying updates, configuring SSH, managing users, and securing remote access.

---

## Security Policy Outline Created for Hardening Process

![security policy pt1](media/securitypolicy1.jpeg)

![security policy pt2](media/securitypolicy2.jpeg)

![security policy pt3](media/securitypolicy3.jpeg)

![security policy pt4](media/securitypolicy4.jpeg)

---

## Tools and Technologies

- **Operating System:** Ubuntu 24.04.1 LTS  
- **Package Management:** APT  
- **Security Tools:** Nmap, OpenSSH, UFW (Uncomplicated Firewall)  
- **Utilities:** SSH, Nano, Systemctl  

---

## System Updates and Package Installation

### Description  
Updated the system and installed necessary packages using APT to enhance security and functionality.

### Commands Used  
```bash
sudo apt update  
sudo apt upgrade  
sudo apt autoremove  
sudo apt clean  
sudo apt install openssh-server
```


### Installed Packages  
- OpenSSH Server for secure remote access.

  
![ubuntuhardeningscrn1](media/ubuntuhardeningscrn1.png)

---

## User Management

### Description  
Managed user accounts by adding, and assigning minimal permissions to ensure least privilege.

### Commands Used  
```bash
sudo adduser 
sudo usermod -aG sudo 
sudo passwd 
```
![ubuntuhardeningscrn2](media/ubuntuhardeningscrn2.png)

---

## Configuring Hostname

### Description  
Changed the system’s hostname for easier identification.

### Commands Used
```bash
hostname  
sudo hostname  
```
![ubuntuhardeningscrn2](media/ubuntuhardeningscrn3.png)

I changed the hostname to ddr7 just because...

---

# Securing Remote Access (SSH)

## Part A: Generate SSH Keys

### Description  
Got IP address, generated and installed SSH keys for secure, passwordless login.

### Commands Used  
```bash
hostname -I
ssh-keygen  
ssh-copy-id user@your_ubuntu_ip
```
![ubuntuhardeningscrn2](media/IMG_7382.jpeg)

I won't post my SSH key for the world to see so here's a picture of one of my favorite japanese dogs :)
   
## Part B: Disable Password Authentication and Root Login

### Description  
Configured SSH to enforce key-based authentication and disabled direct root login.

### Commands Used  
Edited SSH configuration file & restarted SSH
```bash
sudo nano /etc/ssh/sshd_config

PasswordAuthentication no  
PermitRootLogin no

sudo systemctl restart ssh  
```
![ubuntuhardeningscrn2](media/ubuntuhardeningscrn4.png)

---

## Key Accomplishments

- Hardened the Ubuntu system against unauthorized access.
- Configured network monitoring with Nmap and net-tools.
- Implemented SSH key-based authentication to enhance remote access security.

---

## Challenges and Solutions

### Challenge 1: SSH key-based authentication failed during initial setup.  
**Solution:** Corrected `.ssh` directory permissions on the client and server.

### Challenge 2: Incomplete Nmap results due to firewall rules.  
**Solution:** Adjusted firewall to allow full network scans temporarily for documentation.

---

## Reflection and Future Improvements

### Reflection  
This project deepened my understanding of system hardening, secure remote access, and network monitoring.

### Future Improvements  
- Automate package updates and user management with shell scripts.  
- Integrate with SIEM tools for advanced log analysis.

---

## Sample Code and Configuration

```bash
# System update and package installation
sudo apt update && sudo apt upgrade -y
sudo apt install openssh-server nmap net-tools
```

```plaintext
# Example SSH Configuration Changes
PasswordAuthentication no
PermitRootLogin no
```

---

## Definitions

<dl>
<dt>Linux</dt>
<dd>An open-source operating system kernel used in various computing environments.</dd>
<dt>Network Map</dt>
<dd>A visual or textual representation of devices and their connections within a network.</dd>
<dt>SSH</dt>
<dd>Secure Shell, a protocol for secure remote login and communication over a network.</dd>
</dl>

---

## Conclusion

This project demonstrates the process of securing an Ubuntu system through hardening practices. The network map and SSH configuration are crucial components for maintaining a secure infrastructure.
"""
