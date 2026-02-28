# System Overview

## Purpose of This Lab
This system is a personal blue team lab designed to practice defensive security skills,
including system hardening, logging, detection, and incident response.
The goal is to simulate defending a real endpoint with limited resources,
similar to junior SOC or system defender environments.

---

## System Information
- **Operating System:** MX Linux (Debian-based)
- **Kernel Version:** 6.12.63+deb13-amd64
- **Architecture:** x86_64
- **Hardware:** Old personal computer (non-virtualized)
- **Role:** Single Linux endpoint

---

## Environment Type
- Standalone system
- Not domain-joined
- No centralized SIEM
- Logs stored locally

This reflects small-scale or entry-level production environments
where blue teamers must work without enterprise tooling.

---

## Installed Security-Relevant Components
- UFW (firewall)
- OpenSSH (remote access)
- systemd journaling
- Local user authentication

Additional defensive tools will be added incrementally.

---

## Assumptions
- System is assumed to be internet-connected
- Attacker may reach exposed network services
- Attacker does not have initial credentials
- Defender has full administrative access

---

## Scope
### In Scope
- Host-based security
- Network exposure
- Authentication events
- Log analysis
- Detection and response

### Out of Scope
- Active exploitation
- Malware development
- Red team tooling
- Windows or AD environments

---

## Defender Goals
- Reduce attack surface
- Increase visibility through logs
- Detect unauthorized access
- Respond to common attack scenarios
- Document findings clearly and professionally
