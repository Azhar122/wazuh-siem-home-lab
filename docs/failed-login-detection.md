# Failed Login Detection

## Objective

Generate a controlled failed Windows login and confirm that the event is collected and displayed by Wazuh.

## Detection Flow

```text
Failed Windows login
→ Windows Security Event 4625
→ Wazuh Agent
→ Wazuh Manager
→ Wazuh Dashboard
```

## Test Procedure

1. Confirmed that Windows failure auditing was enabled.
2. Generated a controlled login attempt using an incorrect password.
3. Verified Event ID `4625` in the Windows Security log.
4. Located the corresponding event in Wazuh Threat Hunting.
5. Reviewed the account name, failure reason, logon type, source address and Wazuh rule information.

## Results

Wazuh successfully detected and displayed the failed authentication event.

| Field | Result |
|---|---|
| Windows Event ID | 4625 |
| Event type | Failed logon |
| Data source | Windows Security log |
| Detection status | Successfully detected |
| Monitored endpoint | Windows 11 laptop |

## Investigation Fields

The following fields were reviewed:

- Failed account name
- Failure reason
- Logon type
- Source address
- Process name
- Wazuh rule ID
- Wazuh rule level
- Event timestamp

## Learning Outcome

This lab demonstrated how Windows authentication events are generated locally, collected by the Wazuh agent and analysed through the SIEM dashboard.

It also showed the importance of verifying the original Windows event before troubleshooting event collection in Wazuh.