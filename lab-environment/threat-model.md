# Threat Model

## Purpose
This document outlines realistic threat scenarios for the blue team lab system.
The goal is to prioritize defensive efforts based on likely attacker behavior,
system exposure, and potential impact.

---

## Asset Description
- Single Linux endpoint
- Internet-connected
- Used by a single user
- Contains limited personal files
- No sensitive enterprise data

---

## Threat Actors

### 1. Opportunistic Internet Attackers
- Scan IP ranges for exposed services
- Attempt brute-force authentication (e.g. SSH)
- No specific target interest

### 2. Low-Skill Scripted Attackers
- Use automated tools
- Focus on default credentials and misconfigurations
- Limited persistence capability

---

## Attack Vectors

- Remote network services (e.g. SSH)
- Weak authentication mechanisms
- Misconfigured firewall rules
- Unpatched system components

---

## Attacker Goals

- Gain unauthorized access
- Establish persistence
- Use system resources (e.g. botnet, crypto-mining)
- Exfiltrate any accessible data

---

## Defensive Priorities

1. Reduce exposed attack surface
2. Harden authentication mechanisms
3. Monitor and analyze authentication logs
4. Detect and block brute-force attempts
5. Respond quickly to suspicious activity

---

## Assumptions and Limitations

- No advanced targeted attacks assumed
- No insider threat considered
- No zero-day exploitation in scope
- Focus on common, real-world attacks

---

## Review Notes
This threat model will be updated as additional services,
exposures, and defensive controls are identified.
