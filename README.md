# SOC Security Monitoring Lab (Wazuh SIEM)

## Overview
This project demonstrates a Security Operations Center (SOC) monitoring environment using Wazuh SIEM. The lab collects logs from Linux endpoints and detects suspicious activities such as SSH brute-force attempts and network scanning.

## Architecture

Ubuntu Server (Wazuh Manager + Dashboard)
|
|---- Ubuntu Endpoint (Wazuh Agent)

## Tools Used
- Wazuh SIEM
- Ubuntu Linux
- VirtualBox
- Nmap
- SSH

## Security Scenarios Simulated
1. Network reconnaissance using Nmap
2. SSH brute-force login attempts
3. Log monitoring and alert detection

## Screenshots

### Wazuh Dashboard
![Dashboard](screenshots/wazuh-dashboard.png)

### Agent Deployment
![Agent](screenshots/deploy-agent.png)

### Agent Connected
![Agent Connected](screenshots/agent-connected.png)

### Security Alerts Detected
![Alerts](screenshots/security-alerts.png)

## Demo
Watch the lab demonstration:

demo/soc-demo.mp4

## Learning Outcomes
- Security monitoring using SIEM
- Endpoint log collection
- Incident detection
- Threat investigation workflow
