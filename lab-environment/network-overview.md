# Network Overview

## Purpose
This document describes the network exposure of the blue team lab system.
Understanding network connectivity is critical for assessing attack surface
and prioritizing defensive controls.

---

## Network Connectivity
- System is connected to the internet
- Uses a single network interface
- Receives network configuration via DHCP
- No port forwarding configured on the router

---

## Network Interfaces
- One active interface used for outbound and inbound traffic
- No wireless access point or bridging enabled
- No additional virtual interfaces

---

## Firewall Status
- Host-based firewall: UFW
- Default policy: deny incoming, allow outgoing
- Firewall rules are documented separately

---

## Exposure Level
- System is directly exposed to the internet
- Only explicitly allowed services are reachable
- Network exposure is minimized through firewall controls

---

## Defensive Notes
- Network exposure is limited to required services only
- Firewall rules will be reviewed and adjusted as services change
- Network configuration changes will be documented
