# Wazuh SIEM Home Lab

A controlled Wazuh SIEM home lab built to practise endpoint monitoring, log analysis, file integrity monitoring, troubleshooting, and basic security-event investigation.

## Project Overview

This project documents the deployment of a small Wazuh SIEM environment using an Ubuntu Server virtual machine as the central Wazuh server and a Windows 11 laptop as the monitored endpoint.

The lab was created for practical learning and does not represent a production deployment.

## Objectives

- Deploy a functional Wazuh SIEM environment
- Connect and monitor a Windows endpoint
- Understand agent enrolment and communication
- Configure File Integrity Monitoring
- Detect file creation, modification, and deletion
- Investigate alerts using the Wazuh dashboard
- Practise Linux, Windows, network, and service troubleshooting
- Build a foundation for SOC analysis and detection engineering

## Lab Architecture

```text
Windows 11 Laptop
└── Wazuh Agent
        │
        │ TCP 1514
        ▼
Ubuntu Server VM
├── Wazuh Manager
├── Filebeat
├── Wazuh Indexer
└── Wazuh Dashboard



| Component          | Technology                 |
| ------------------ | -------------------------- |
| Hypervisor         | Oracle VirtualBox          |
| SIEM server        | Ubuntu Server 24.04 LTS    |
| SIEM platform      | Wazuh 4.12.0               |
| Monitored endpoint | Windows 11                 |
| Endpoint agent     | Wazuh Agent 4.12.0         |
| Networking         | VirtualBox Bridged Adapter |
| Administration     | SSH and PowerShell         |




|  Port | Purpose                   |
| ----: | ------------------------- |
|    22 | SSH administration        |
|   443 | Wazuh dashboard           |
|  1514 | Agent event communication |
|  1515 | Agent enrolment           |
|  9200 | Wazuh indexer             |
| 55000 | Wazuh API                 |


Completed Work
Wazuh Deployment

Installed the Wazuh manager, indexer, dashboard, and Filebeat on an Ubuntu Server virtual machine.

Windows Agent Deployment

Installed and registered a Wazuh agent on a Windows 11 laptop and verified communication between the endpoint and the manager.

File Integrity Monitoring

Configured real-time monitoring for a controlled Windows folder.



| Action        | FIM event | Wazuh rule ID |
| ------------- | --------- | ------------: |
| File created  | Added     |           554 |
| File modified | Modified  |           550 |
| File deleted  | Deleted   |           553 |


Troubleshooting Experience

Several problems occurred during the deployment:


| Problem                                | Root cause                                  | Resolution                                                                                 |
| -------------------------------------- | ------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Agent service stopped                  | Manager address was configured as `0.0.0.0` | Updated the manager address in `ossec.conf`                                                |
| Agent remained pending                 | Agent version was newer than the manager    | Reinstalled the matching Wazuh 4.12.0 agent                                                |
| Agent lost connectivity                | Ubuntu lost its bridged IPv4 address        | Corrected the VirtualBox network adapter                                                   |
| Dashboard could not access stored data | The indexer was not listening on port 9200  | Verified and restored the indexer service                                                  |
| Manager failed to start                | A stale startup lock remained               | Confirmed no manager process was active, removed the stale lock, and restarted the service |


## Skills Practised
- SIEM deployment
-Wazuh administration
-Windows event monitoring
-File Integrity Monitoring
-Linux service management
-PowerShell
-SSH
-Network troubleshooting
-Log analysis
-Agent enrolment
-Security-alert investigation



##Repository Structure:

wazuh-siem-homelab/
├── README.md
├── configs/
│   └── ossec.conf.example
├── docs/
│   ├── architecture.md
│   ├── installation.md
│   ├── agent-deployment.md
│   ├── fim-lab.md
│   ├── failed-login-detection.md
│   └── troubleshooting.md
└── images/


## Future Work
-Complete failed-login detection
-Integrate Sysmon
-Monitor process creation and PowerShell activity
-Review Security -Configuration Assessment results
-Review vulnerability-detection results
-Create a custom Wazuh rule
-Perform a controlled incident investigation
-Write a SOC incident report


## Security Notice

Passwords, API credentials, agent keys, authentication tokens, certificates, and private SSH keys have been excluded from this repository.