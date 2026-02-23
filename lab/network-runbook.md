# VMware Fusion Runbook

## Objective

Maintain a clean, repeatable baseline for the two-zone lab:

- `corp` (`10.10.10.0/24`) → Kali
- `server` (`10.10.20.0/24`) → Ubuntu server + Ubuntu SIEM server
- Ubuntu router VM provides controlled inter-zone routing

---

## Current State (Completed)

- Two custom VMware networks created (`corp`, `server`)
- Kali deployed with dual NICs:
  - `corp` NIC
  - NAT/management NIC (internet/package access)
- Ubuntu server deployed with dual NICs:
  - `server` NIC
  - NAT/management NIC (internet/package access)
- SIEM VM deployed with dual NICs:
  - NAT/management NIC (internet/package access)
  - `server` NIC
- Router VM configured with:
  - `10.10.10.1/24` (corp side)
  - `10.10.20.1/24` (server side)

Segmentation + routed connectivity are functioning for Week 2 SIEM rollout.

---

## Fast Verification Commands

### Kali

```bash
ip a
ip route
ping -c 3 10.10.10.1
ping -c 3 10.10.20.10
```

### Ubuntu server (`lab-srv-01`)

```bash
ip a
ip route
ping -c 3 10.10.20.1
ping -c 3 10.10.10.10
```

### SIEM server (`lab-siem-01`)

```bash
df -h /
ip -br a
ip route
ping -c 3 10.10.20.1
ping -c 3 10.10.20.10
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

## Change Records

### Change Record - 2026-02-21

- Change: Built `lab-siem-01`, added second NIC, adjusted disk size, baseline connectivity verification.
- Why: Needed dedicated SIEM compute and stable network path before Wazuh install.
- Before: No SIEM VM in server zone.
- After: SIEM VM reachable in server zone (`10.10.20.20`) with package install path via mgmt NAT.
- Validation commands: `ip -br a`, `ip route`, `ping -c 3 10.10.20.1`, `ping -c 3 10.10.20.10`, `df -h /`.
- Result: Connectivity and resized storage verified.
- Rollback plan: Revert to pre-install VM snapshot and reapply NIC/disk settings.

### Change Record - 2026-02-22

- Change: Installed Wazuh all-in-one stack on `lab-siem-01`, deployed Wazuh agent to Ubuntu server.
- Why: Start SIEM telemetry onboarding for Week 2 objectives.
- Before: Segmented network existed but no active SIEM ingestion pipeline.
- After: Wazuh dashboard up; Ubuntu server agent active; baseline events visible in Threat Hunting.
- Validation commands:
    -`systemctl status wazuh-dashboard wazuh-manager wazuh-indexer`, `systemctl status wazuh-agent --no-pager` (on Ubuntu server).
  - Dashboard Endpoints + Threat Hunting checks.
- Result: Basic ingestion validated.
- Rollback plan: Restore snapshots and remove Wazuh packages if service instability occurs.

---

## What to finalize next

1. Enable and validate router log forwarding to SIEM.
2. Onboard Kali logs (agent or syslog-forward path).
3. Define minimal network control policy between `corp` and `server`.
4. Capture sanitized screenshots and architecture diagram for public repo evidence.
