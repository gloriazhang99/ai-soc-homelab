# Lab Asset Inventory

## Network Zones

| Zone | CIDR | Purpose |
|---|---|---|
| `corp` | `10.10.10.0/24` | User/attacker simulation zone |
| `server` | `10.10.20.0/24` | Server/log source + SIEM zone |

---

## Active Assets

| Asset            | Role                     | OS                  | Interface(s)                             | Zone               | Current IP                         | Gateway       | Assignment |
|------------------|--------------------------|---------------------|------------------------------------------|--------------------|------------------------------------|------------------------------------------|------------|
| Kali VM (`lab-attk-01`)  | Attack simulation host   | Kali Linux (2025.4) | `eth0`                                   | `corp`             | `10.10.10.10/24`                   | `10.10.10.1`  | Static     |
| Ubuntu VM (`lab-srv-01`) | Linux server/log source  | Ubuntu 22.04.5 LTS  | `ens160`                                 | `server`           | `10.10.20.10/24`                   | `10.10.20.1`  | Static     |
| Ubuntu VM (`lab-rtr-01`) | Inter-zone router        | Ubuntu 22.04.4 LTS  | `ens256` (corp), `ens161` (server)       | `corp` + `server`  | `10.10.10.1/24`, `10.10.20.1/24`   | N/A           | Static     |
| Ubuntu VM (`lab-siem-01`)| SIEM server (Wazuh)      | Ubuntu 22.04.4 LTS  | `ens256` (server)   | `server`   | `10.10.20.20/24`      | `10.10.20.1`  | Static      |

---

## Validation Evidence (Latest)

- `lab-siem-01` validated dual-NIC network path and server-zone reachability.
- Wazuh manager/indexer/dashboard services confirmed active on `lab-siem-01`.
- Ubuntu server agent (`lab-srv-01`) deployed and shown as active in Wazuh Endpoints.
- Basic endpoint event ingestion validated in Wazuh Threat Hunting.

---

## Missing Info to Fill (Quick Checklist)

- [ ] Record SIEM VM exact mgmt-side addressing details and DHCP lease source.
- [ ] Add snapshot names + timestamps for post-SIEM deployment restore points.
- [ ] Record retention/storage plan for Wazuh indices on current disk size.
- [ ] Add router logging export configuration once forwarded to SIEM.
- [ ] Add Kali logging source onboarding details (agent/syslog approach).

---

## Next Actions

1. Ingest router logs into Wazuh and validate parser mapping.
2. Ingest Kali endpoint logs and validate host-level fields.
3. Define a normalized field baseline for triage (`host`, `src.ip`, `dst.ip`, `user`, `event.action`, `severity`).
4. Build dashboard panels for endpoint health, authentication events, and high-severity alerts.
