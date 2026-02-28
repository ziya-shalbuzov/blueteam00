# Open Ports Enumeration

## Purpose
This document identifies network-exposed services on the system and evaluates
their security impact. Open ports represent potential attack vectors and must
be minimized and justified.

---

## Enumeration Method
Command used:
```bash
sudo ss -tulpen
```

## Findings
- chronyd service present for system time synchronization
- UDP port 323 bound to localhost for chrony control
- No unnecessary TCP or UDP services listening on external network interfaces
- No unauthorized or unexpected network-exposed services observed

## Risk Assessment
- chronyd is required for accurate system time and reliable log timestamps
- Local-only control interfaces do not present remote attack vectors
- Overall network attack surface is minimal after service hardening

## Defensive Actions
### avahi-daemon (mDNS):
Disabled to remove service discovery exposure.
```bash
sudo service avahi-daemon stop
sudo update-rc.d avahi-daemon disable
```
### rpcbind and RPC/NFS services:
Disabled to eliminate common RPC-based attack targets.
```bash
sudo service rpcbind stop
sudo update-rc.d rpcbind disable
```

```bash
sudo service nfs-common stop
sudo update-rc.d nfs-common disable
```
### saned (Scanner daemon):
Disabled to prevent remote scanner access.
```bash
sudo service saned stop
sudo update-rc.d saned disable
```
### Printing services (cups):
Reviewed and disabled where not required.
```bash
sudo service cups stop
sudo update-rc.d cups disable
```
### Verification:
Attack surface reduction verified.
```bash
sudo ss -tulpen
```

## Environment Notes
- MX Linux uses SysVinit rather than systemd
- Service management performed using service and update-rc.d
- Enumeration and hardening steps were adapted accordingly
