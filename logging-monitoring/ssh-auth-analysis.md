# SSH Authentication Log Analysis

## Purpose
Analyze SSH authentication activity on the MX Linux host to:
- Establish a baseline of normal SSH behavior
- Detect suspicious authentication patterns
- Support incident triage using log evidence
This analysis is written from a defensive SOC perspective.

---

## Environment Context
- OS: MX Linux (Debian-based)
- SSH Server: OpenSSH (`sshd`)
- SSH installed intentionally for monitoring practice
- Service management via `service` (not systemctl)

### Verification
```bash
service ssh status
ss -tulpn | grep :22
```

---

## Log Source
- Primary log: /var/log/auth.log
- Relevant process: sshd
The auth.log file records authentication events including SSH, sudo, and other security-relevant actions.

---

## SSH Events of Interest
Common SSH authentication events observed in logs:
- Accepted password for <user> from <ip>
- Accepted publickey for <user> from <ip>
- Failed password for <user> from <ip>
- Invalid user <user> from <ip>
- Disconnected from <ip>
- sudo: (post-login privilege escalation)

---

## Baseline Behavior (Lab)
### Baseline SSH activity observed:
Successful logins only from:
- Local user
- Source IP: 127.0.0.1

Authentication method:
- Password-based (lab testing)

Login frequency:
- Low, manual, intentional

Failed logins:
- Occasional mistyped passwords
- No high-volume failures

---

## Baseline Queries
Successful logins:
```bash
grep "sshd.*Accepted" /var/log/auth.log
```

Failed logins:
```bash
grep "sshd.*Failed password" /var/log/auth.log
```

---

## Detection Logic
### Brute Force Indicators
Suspicious if:
- High number of Failed password events
- Same source IP repeated frequently
- Failures across multiple user accounts

Query:
```bash
grep "sshd.*Failed password" /var/log/auth.log \
 | awk '{for(i=1;i<=NF;i++) if($i=="from") print $(i+1)}' \
 | sort | uniq -c | sort -nr
```

---

## Username Enumeration
Suspicious if:
- Repeated Invalid user entries
- Sequential or common usernames targeted

Query:
```bash
grep "sshd.*Invalid user" /var/log/auth.log
```

Interpretation:
- Likely reconnaissance or automated scanning

---

## Suspicious Successful Logins
Suspicious if:
- Login from unknown IP
- Login outside normal hours
- Login followed by sudo usage

Query:
```bash
grep "sshd.*Accepted" /var/log/auth.log
```

---

## Post-Login Privilege Escalation
SSH compromise is often followed by privilege escalation.

Query:
```bash
grep "sudo:" /var/log/auth.log
```

SOC focus:
- Correlate SSH login → sudo usage
- Identify unexpected elevation attempts

---

## Observed Lab Events (Controlled)
The following events were intentionally generated to validate logging:
### Successful Login
- Event: Accepted password
- User: local user
- Source IP: 127.0.0.1
- Interpretation: Normal baseline activity

### Failed Password
- Event: Failed password
- User: local user
- Source IP: 127.0.0.1
- Interpretation: Benign authentication error

### Invalid User Attempt
- Event: Invalid user fakeuser
- Source IP: 127.0.0.1
- Interpretation: Username enumeration behavior

---

## Incident Triage Checklist
When suspicious SSH activity is detected:
- Identify source IP(s)
- Count failed authentication attempts
- Check for successful logins from same IP
- Identify targeted user accounts
- Look for sudo usage after login

## Notes
- SSH monitoring is currently manual
- Automated detection and blocking will be implemented later using Fail2ban
- This file serves as the analytical foundation for future detection engineering
