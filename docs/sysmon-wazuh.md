# Sysmon Integration with Wazuh

## Objective

Extend the Wazuh home lab with Sysmon telemetry to gain deeper visibility into Windows processes, registry activity, process access, and other endpoint events.

## Setup

Sysmon was installed on the Windows endpoint and configured to write events to:

`Microsoft-Windows-Sysmon/Operational`

The Wazuh agent was configured to collect this event channel:

```xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

## Verification

Sysmon events were first confirmed locally using PowerShell:

```powershell
Get-WinEvent `
  -LogName "Microsoft-Windows-Sysmon/Operational" `
  -MaxEvents 10
```

The same Sysmon telemetry was then observed in Wazuh Threat Hunting.

This confirmed the pipeline:

```text
Windows Activity
      ↓
Sysmon
      ↓
Windows Event Log
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Indexer
      ↓
Dashboard
```

## Alert Investigation

Wazuh generated a level 12 alert:

* Wazuh Rule: `92910`
* Sysmon Event ID: `10`
* MITRE ATT&CK: `T1055 - Process Injection`
* Source: `OmenCommandCenterBackground.exe`
* Target: `Explorer.EXE`

The alert indicated possible process injection behavior.

### Investigation

The source executable was verified to:

* Have a valid digital signature from HP Inc.
* Exist inside the expected WindowsApps installation directory.
* Belong to the intentionally installed OMEN Gaming Hub application.
* Run as a persistent background process.

Sysmon showed 216 matching process-access events over approximately 24 hours.

The events followed a consistent recurring pattern between the same OMEN process and Windows Explorer.

## Conclusion

The alert was classified as a **benign positive**.

The suspicious behavior was genuinely observed, but investigation showed that it originated from legitimate installed software.

No suppression rule was created because further monitoring is preferable to prematurely whitelisting the activity.

## Key Learning

A high-severity SIEM alert does not automatically mean that a system is compromised.

The correct workflow is:

```text
Alert
  ↓
Validate telemetry
  ↓
Investigate process and context
  ↓
Correlate evidence
  ↓
Classify
```

Suggested screenshot:

```text
images/sysmon-wazuh-alert.png
```
