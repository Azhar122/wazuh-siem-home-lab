# Lab Architecture

The lab uses one Ubuntu Server VM as a central Wazuh Server and one Windows 11 laptop as the monitored endpoint.

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
```

## Component Roles

- Wazuh Agent - Collects Windows logs, system info and FIM events
- Wazuh Manager - Recieves and analyses endpoint events
- Filebeat - Forwards generated alerts to the indexer
- Wazuh Indexer - Stores and searches security alerts
- Wazuh Dashboard - The web interface for monitoring and investigating

## Network Design

VirtualBox bridged networking placees the Ubuntu VM and the Windows laptop on the same local network. 

Ports:
- Port 22 - SSH admin
- Port 443 - Wazuh dashboard
- 1514 - Agent Communication
- 1515 - Agent enrolment
- 9200 - Wazuh indexer
- 55000 - Wazuh API
