# SOC Security Monitoring Lab – Setup Guide

## Overview

This guide explains how to build a **SOC Security Monitoring Lab using Wazuh SIEM**.
The lab simulates a Security Operations Center where security events from endpoints are monitored and analyzed.

In this project we:

* Deploy a **Wazuh SIEM server**
* Install a **Wazuh agent on an Ubuntu endpoint**
* Simulate attacks using **SSH brute force and Nmap scans**
* Detect and analyze alerts using the **Wazuh dashboard**

---

# 1. Environment Setup

### Host Machine

* Windows 11
* Oracle VirtualBox

### Virtual Machines

| VM            | Purpose                     |
| ------------- | --------------------------- |
| Ubuntu Server | Wazuh SIEM Server           |
| Ubuntu Agent  | Endpoint monitored by Wazuh |

---

# 2. Install VirtualBox

Download and install:

[https://www.virtualbox.org/](https://www.virtualbox.org/)

---

# 3. Create Ubuntu Virtual Machine

Download Ubuntu Server ISO:

[https://ubuntu.com/download/server](https://ubuntu.com/download/server)

In VirtualBox create a new VM:

```
Name: Ubuntu-Wazuh
Type: Linux
Version: Ubuntu (64-bit)

RAM: 4 GB
CPU: 2 cores
Disk: 40 GB
```

Install Ubuntu normally.

---

# 4. Update Ubuntu Server

After installation log in and run:

```bash
sudo apt update
sudo apt upgrade -y
```

---

# 5. Install Wazuh SIEM Server

Run the Wazuh installation script:

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

This installs:

* Wazuh Manager
* Elasticsearch
* Wazuh Dashboard

---

# 6. Access Wazuh Dashboard

Find the server IP address:

```bash
ip a
```

Open the dashboard in a browser:

```
https://SERVER-IP
```

Login with the credentials generated during installation.

---

# 7. Deploy Wazuh Agent

Open the **Wazuh Dashboard**.

Navigate to:

```
Agents → Deploy New Agent
```

Choose:

```
Operating System: Linux
Server Address: <Wazuh Server IP>
Agent Name: ubuntu-agent
```

Copy the generated installation command.

Example:

```bash
sudo apt install wazuh-agent
```

---

# 8. Start the Agent

Start and enable the agent:

```bash
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

Verify the agent status:

```bash
sudo systemctl status wazuh-agent
```

---

# 9. Register Agent With Server

Authenticate the agent with the Wazuh server:

```bash
sudo /var/ossec/bin/agent-auth -m <SERVER-IP>
```

Example:

```bash
sudo /var/ossec/bin/agent-auth -m 192.168.0.22
```

Restart the agent:

```bash
sudo systemctl restart wazuh-agent
```

---

# 10. Verify Agent Connection

Go to the dashboard:

```
Endpoints → Agents
```

You should see:

```
Agent: ubuntu-agent
Status: Active
```

---

# 11. Attack Simulation

To generate security alerts we simulate attacks.

### SSH Brute Force

Run multiple login attempts:

```bash
ssh fakeuser@localhost
```

Repeat several times to trigger alerts.

---

### Nmap Scan

Simulate reconnaissance activity:

```bash
sudo apt install nmap
sudo nmap -sS <SERVER-IP>
```

Example:

```bash
sudo nmap -sS 192.168.0.22
```

---

# 12. View Security Alerts

Go to the Wazuh dashboard:

```
Threat Hunting → Events
```

Detected alerts may include:

* SSH login attempts
* Brute force attacks
* Failed authentication
* Privilege escalation

---

# 13. Security Analysis

Wazuh provides visibility into:

* **MITRE ATT&CK techniques**
* **Authentication failures**
* **System vulnerabilities**
* **File integrity monitoring**
* **Security configuration assessments**

---

# Lab Outcome

This SOC lab demonstrates how security analysts:

* Monitor endpoints
* Detect suspicious activity
* Analyze security alerts
* Investigate attack behavior

---

# Tools Used

* Wazuh SIEM
* Ubuntu Server
* Oracle VirtualBox
* SSH
* Nmap


