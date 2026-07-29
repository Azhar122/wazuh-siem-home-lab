# Wazuh Server Installation

## Environment

- Ubuntu Server 24.04 LTS
- Oracle VirtualBox
- Wazuh 4.12.0 all-in-one installation
- Bridged network adapter

## Installation Summary

The Wazuh installation assistant was used to install:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard 
- Filebeat

The dashboard was accessed fromt eh Windows laptop using the Ubuntu VM's local IPv4 address:

```text
https://WAZUH-MANAGER-IP
```

## Service Verification

The main services were checked using:

```bash
sudo systemctl is-active \
  wazuh-manager \
  wazuh-indexer \
  wazuh-dashboard \
  filebeat
```


A healthy deployment shoudl show all services as 'active'.

