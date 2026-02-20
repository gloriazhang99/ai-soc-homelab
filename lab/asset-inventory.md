# Lab Asset Inventory

## Network Zones

| Zone | CIDR | Purpose |
|---|---|---|
| `corp` | `10.10.10.0/24` | User/attacker simulation zone |
| `server` | `10.10.20.0/24` | Server/log source zone |

---

## Active Assets

| Asset            | Role                    | OS                 | Interface(s)              | Zone          | Current IP                | Gateway    | Status            | Assignment |
|------------------|-------------------------|--------------------|---------------------------|---------------|---------------------------|------------|-------------------|------------|
| Kali VM          | Attack simulation host   | Kali Linux (2025.4) | `eth0`                    | `corp`        | `10.10.10.10/24`          | `10.10.10.1` | Routing validated | Static     |
| Ubuntu VM        | Linux server/log source  | Ubuntu 22.04.05 LTS | `ens160`                  | `server`      | `10.10.20.10/24`          | `10.10.20.1` | Routing validated | Static     |
| lab-rtr-01       | Inter-zone router        | Ubuntu 22.04.4 LTS  | `ens256` (corp), `ens161` (server) | `corp` + `server` | `10.10.10.1/24`, `10.10.20.1/24` | N/A        | Routing enabled   | Static     |

---

## Validation Evidence (Latest)

- Kali successfully pinged router gateway `10.10.10.1`.
- Kali successfully pinged Ubuntu host `10.10.20.10`.
- Ubuntu successfully pinged router gateway `10.10.20.1`.
- Ubuntu successfully pinged Kali host `10.10.10.10`.
- Router interface summary showed both zone IPs assigned (`10.10.10.1/24`, `10.10.20.1/24`).

---

## Missing Info to Fill (Quick Checklist)

- [ ] Ubuntu exact OS version (`cat /etc/os-release`)
- [ ] Kali exact release metadata (`cat /etc/os-release`)
- [ ] Snapshot names + timestamps after routing success
- [ ] Confirm whether endpoints are DHCP or static in final state
- [ ] Record `ip route` output for each VM (for incident baseline)

---

## Next Actions

1. Add minimal router policy (allow only needed traffic across zones).
