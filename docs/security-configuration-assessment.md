# Security Configuration Assessment

## Objective

Use Wazuh Security Configuration Assessment (SCA) to identify insecure Windows configuration settings and apply selected hardening changes.

SCA differs from vulnerability detection:

```text
Vulnerability Detection
→ Is installed software vulnerable?

Security Configuration Assessment
→ Is the system configured securely?
```

## Password Policy Findings

Wazuh identified several CIS password-policy checks.

### Password History

Initial state:

```text
Length of password history maintained: None
```

CIS recommendation:

```text
24 previous passwords
```

Remediation:

```powershell
net accounts /uniquepw:24
```

Result:

```text
Length of password history maintained: 24
```

### Minimum Password Age

Initial state:

```text
Minimum password age: 0 days
```

Remediation:

```powershell
net accounts /minpwage:1
```

Result:

```text
Minimum password age: 1 day
```

This prevents users from rapidly cycling through passwords to bypass password-history controls.

### Maximum Password Age

The existing value was:

```text
Maximum password age: 42 days
```

The Wazuh CIS check required a value of 365 days or fewer, but not zero.

Therefore, this check already passed and no remediation was required.

### Minimum Password Length

Initial state:

```text
Minimum password length: 0
```

The benchmark recommended:

```text
14 or more characters
```

The setting was hardened to require a minimum password length of 14 characters.

## Final Local Policy

After remediation:

```text
Minimum password age:              1 day
Maximum password age:              42 days
Minimum password length:           14 characters
Password history maintained:       24 passwords
Lockout threshold:                 10 attempts
Lockout duration:                  10 minutes
Lockout observation window:        10 minutes
```

## Key Learning

A failed compliance check should not be blindly remediated.

The process should be:

```text
Finding
  ↓
Understand the recommendation
  ↓
Evaluate impact
  ↓
Remediate or accept
  ↓
Verify locally
  ↓
Verify through Wazuh
```

Security benchmarks provide a baseline, but system requirements and operational context must also be considered.
