# Windows Agent Deployment

## Overview 

A Wazuh 4.12.0 agent was installed on the windows 11 laptop and registered with teh ubuntu Wazuh manager.

The agent version was kept equal to the manager version because Wazuh agent cannot be newer than its manager.

## Configuration

The manager address was configured in:

```text
C:\Program Files (x86)\ossec-agent\ossec.conf
```

Example:

```xml
<client>
  <server>
    <address>WAZUH-MANAGER-IP</address>
  </server>
</client>
```

The agent registration key was imported using Wazuh Agent Manager.

## Verification

The Windows service was checked using Administrator PowerShell:

```powershell
Get-Service WazuhSvc
```

The agent connection was verified through:

```powershell
Get-Content "C:\Program Files (x86)\ossec-agent\ossec.log" -Tail 30
```

A successful connection included:

```text
Connected to the server
Agent is now online
```

The manager also displayed the endpoint as `Active`.