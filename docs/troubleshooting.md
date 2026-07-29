# Troubleshooting Notes

Several issues occurred during the lab and were diagnosed using service status, logs and network tests.

| Problem | Root Cause | Resolution |
|---|---|---|
| Agent service would not remain running | Manager address was `0.0.0.0` | Updated `ossec.conf` |
| Agent stayed pending | Agent version was newer than manager | Installed Wazuh Agent 4.12.0 |
| Windows could not reach the server | Ubuntu VM lost its bridged IPv4 address | Corrected the bridged adapter |
| Dashboard could not query alerts | Indexer was unavailable on port 9200 | Restored the indexer service |
| Manager failed to start | Stale startup lock remained | Verified no manager process was running and removed the stale lock |

## Useful Commands

Windows connectivity test:

```powershell
Test-NetConnection WAZUH-MANAGER-IP -Port 1514
```

Ubuntu service check:

```bash
sudo systemctl status wazuh-manager
```

Listening ports:

```bash
sudo ss -lntp
```

Windows agent log:

```text
C:\Program Files (x86)\ossec-agent\ossec.log
```

Wazuh manager log:

```text
/var/ossec/logs/ossec.log
```

## Main Lesson

A running process does not prove that the complete system is healthy. Each layer must be verified separately: service, network, authentication and application communication.