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
sudo apt update && sudo apt upgrade -y
sudo apt install openssh-server nmap net-tools
```

### Installed Packages  
- OpenSSH Server for secure remote access.  
- Nmap and Net-tools for network analysis.

---

## User Management

### Description  
Managed user accounts by adding, deleting, and assigning minimal permissions to ensure least privilege.

### Commands Used  
```bash
sudo adduser newuser
sudo deluser username
sudo usermod -aG sudo newuser
```

---

## Network Map

### Description  
Created a network map using Nmap to identify connected devices and services on the network.

### Sample Command and Output  
```bash
sudo nmap -sP 192.168.1.0/24
```

```plaintext
Starting Nmap 7.80 ( https://nmap.org )
Nmap scan report for 192.168.1.1
Host is up (0.00013s latency).
MAC Address: AA:BB:CC:DD:EE:FF (Vendor Name)
```

---

## Securing Remote Access

### Description  
Configured and hardened SSH access by enforcing key-based authentication and disabling password-based login for security.

### Steps Performed  
1. **Generate SSH Key Pair**  
   ```bash
   ssh-keygen
   ```
   
2. **Copy Public Key to Remote Host**  
   ```bash
   ssh-copy-id user@server_ip
   ```

3. **Modify SSH Configuration**  
   Edited `/etc/ssh/sshd_config`:  
   ```plaintext
   PasswordAuthentication no
   PermitRootLogin no
   ```

4. **Restart SSH Service**  
   ```bash
   sudo systemctl restart ssh
   ```

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
