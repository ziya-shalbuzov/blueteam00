# Threat Model

## Purpose
This document defines realistic threat scenarios for the blue team lab system.
The threat model is based on observed attack surface, active services, and
defensive controls applied to the system.

---

## Asset Description
- Single Linux endpoint (MX Linux)
- Internet-connected system
- Used by a single user
- Contains limited personal files
- No enterprise or sensitive business data

---

## Initial Attack Surface (Before Hardening)
- rpcbind (TCP port 111) exposed on all interfaces
- avahi-daemon exposing mDNS service discovery
- saned allowing remote scanner access
- Printing services potentially exposed
- IPv4 and IPv6 network exposure present

These services increased the likelihood of automated scanning and
opportunistic attacks.

---

## Current Attack Surface (After Hardening)
- No unnecessary TCP or UDP services exposed to external networks
- chronyd running for time synchronization with local-only control interface
- All non-essential network services disabled
- Network exposure limited to essential system functions only

Attack surface reduction was verified through repeated enumeration.

---

## Threat Actors

### 1. Opportunistic Internet Attackers
- Perform automated scanning for exposed services
- Target common ports such as RPC/NFS and service discovery protocols
- No specific interest in the system itself

### 2. Low-Skill Script-Based Attackers
- Use publicly available tools
- Exploit default or unnecessary services
- Limited persistence or post-exploitation capability

---

## Attack Vectors

### Prior to Hardening
- RPC service enumeration and exploitation
- Network service discovery via mDNS
- Unauthorized access to scanner services
- Abuse of misconfigured or unnecessary services

### After Hardening
- Network-based attack vectors significantly reduced
- No externally reachable management or discovery services observed
- Remaining attack surface limited to local system access and user behavior

---

## Attacker Goals
- Gain unauthorized access
- Use system resources
- Establish persistence
- Exfiltrate accessible data

Likelihood of success significantly reduced after hardening.

---

## Defensive Priorities
1. Maintain minimal network attack surface
2. Ensure accurate system time for log integrity
3. Monitor authentication and system logs
4. Detect abnormal behavior early
5. Respond quickly to suspicious activity

---

## Assumptions and Limitations
- No advanced targeted attacks assumed
- No insider threat considered
- No zero-day exploitation in scope
- Focus on realistic, common attack techniques

---

## Review Notes
This threat model reflects the current hardened state of the system.
It will be reviewed and updated if new services are introduced or
the system role changes.
