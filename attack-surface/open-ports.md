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
- Disabled avahi-daemon to remove mDNS service discovery exposure
- Disabled rpcbind and related RPC/NFS services to eliminate common attack targets
- Disabled saned to prevent remote scanner access
- Reviewed printing services and disabled where not required
- Verified reduction of exposed services through repeated enumeration

## Environment Notes
- MX Linux uses SysVinit rather than systemd
- Service management performed using service and update-rc.d
- Enumeration and hardening steps were adapted accordingly
