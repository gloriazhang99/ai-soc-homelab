# VMware Fusion Runbook: Segmented Network + Routing

## Objective

Maintain a clean, repeatable baseline for the two-zone lab:

- `corp` (`10.10.10.0/24`) → Kali
- `server` (`10.10.20.0/24`) → Ubuntu
- Ubuntu router VM provides controlled inter-zone routing

---

## Current State (Completed)

- Two custom VMware networks created (`corp`, `server`)
- Kali NIC attached to `corp`
- Ubuntu NIC attached to `server`
- Router VM configured with:
  - `10.10.10.1/24` (corp side)
  - `10.10.20.1/24` (server side)
- Ping validation working:
  - Kali → `10.10.10.1`
  - Kali → Ubuntu (`10.10.20.10`)
  - Ubuntu → `10.10.20.1`
  - Ubuntu → Kali (`10.10.10.10`)

Segmentation + routed connectivity are both functioning.
Snapshots for all VMs created as of Feb 19, 2026.

---

## Fast Verification Commands

### Kali

```bash
ip a
ip route
ping -c 3 10.10.10.1
ping -c 3 10.10.20.10
```

### Ubuntu

```bash
ip a
ip route
ping -c 3 10.10.20.1
ping -c 3 10.10.10.10
```

### Router (Ubuntu)

```bash
ip -br addr
sysctl net.ipv4.ip_forward
```

Expected router result:

- one NIC in `10.10.10.0/24`
- one NIC in `10.10.20.0/24`
- `net.ipv4.ip_forward = 1`

---

## What to finalize next

1.

---

## Fill-in Guide

Template for each time there's a network change:

```md
### Change Record - YYYY-MM-DD
- Change:
- Why:
- Before:
- After:
- Validation commands:
- Result:
- Rollback plan:
```
