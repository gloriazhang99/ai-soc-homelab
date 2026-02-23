# Learning Journal

## Purpose

Track implementation, mistakes, decisions, and lessons.
This mirrors real-world engineering/security run logs.

---

## 2026-02-16

### Time Spent

~3.5 hours

### Goals

- Define practical lab scope that can run reliably on available host resources.
- Draft documentation baseline.

### What I Built

- Wrote initial architecture and repo-structure documentation.
- Scoped project around segmented network + SIEM onboarding first.

### Problems I Hit

- Initial scope too broad (wanted to do SIEM + detections + automation immediately).
- Needed a more realistic phased plan.

### How I Resolved Them

- Converted to week-based plan with explicit milestones.
- Prioritized infrastructure reliability first, then telemetry, then detections/automation.

### Security/Engineering Takeaways

- SOC projects fail when observability is added before stable infrastructure.
- A constrained but measurable scope is better than overpromised architecture.

### Next Steps

- Implement segmented networking (`corp`, `server`) and validate routing.

---

## 2026-02-18

### Time Spent

~4.0 hours

### Goals

- Implement segmented network topology in VMware Fusion.
- Validate host-to-host routed connectivity.

### What I Built

- Created custom networks (`corp`, `server`).
- Configured Kali, Ubuntu server, and Ubuntu router VM NIC mappings.
- Enabled forwarding and validated cross-zone pings.
- Stored routing baseline with snapshots.

### Problems I Hit

- Routing inconsistencies after NIC mapping changes.
- Confusion around final static route/gateway state per VM.

### How I Resolved Them

- Re-validated interface bindings and gateway settings on each VM.
- Added repeatable runbook command set (`ip a`, `ip route`, ping matrix).

### Security/Engineering Takeaways

- Simple network baselines greatly reduce troubleshooting time later.
- Validation matrices are low-cost, high-value evidence.

### Next Steps

- Prepare SIEM VM deployment plan.

---

## 2026-02-20

### Time Spent

~2.5 hours

### Goals

- Prepare Week 2 SIEM rollout approach.
- Align expected telemetry sources with threat-hunting goals.

### What I Built

- Defined SIEM-first Week 2 sequence.
- Identified initial normalized fields needed for triage consistency.

### Problems I Hit

- Needed to keep public documentation useful without exposing sensitive environment detail.

### How I Resolved Them

- Decided to publish only sanitized evidence and non-sensitive architecture details.
- Avoided publishing secrets, tokens, internal usernames, or full management-network specifics.

### Security/Engineering Takeaways

- Good public documentation can still be audit-friendly without exposing operationally sensitive data.

### Next Steps

- Build SIEM VM and install Wazuh.

---

## 2026-02-21

### Time Spent

~4.0 hours

### Goals

- Stand up new Ubuntu SIEM VM (`lab-siem-01`).
- Configure NICs and baseline connectivity.
- Install Wazuh server stack.

### What I Built

- Provisioned `lab-siem-01` with management + server network interfaces.
- Performed VM disk resize and post-change storage verification.
- Installed Wazuh all-in-one stack (manager/indexer/dashboard).
- Verified services are active.

### Problems I Hit

- NIC and route behavior required iterative checks to ensure correct default path and server-zone reachability.
- Needed additional VM storage before proceeding confidently.

### How I Resolved Them

- Used repeated network checks (`ip -br a`, `ip route`, ping tests) before/after changes.
- Resized storage and validated with `df -h /`.

### Security/Engineering Takeaways

- SIEM availability depends as much on host/network reliability as package installation.
- Verifying services (`systemctl status`) immediately after install should be mandatory.

### Next Steps

- Enroll first endpoint agent and confirm event ingestion.

---

## 2026-02-22

### Time Spent

~3.5 hours

### Goals

- Deploy Wazuh agent on Ubuntu server (`lab-srv-01`).
- Validate endpoint registration and baseline telemetry ingestion.

### What I Built

- Installed and started Wazuh agent on Ubuntu server.
- Confirmed agent appears as active in Wazuh Endpoints.
- Confirmed basic logs/events visible in Threat Hunting.

### Problems I Hit

- Initial validation had to distinguish service health from real ingestion success.

### How I Resolved Them

- Validated both layers:
  - service/process health (`systemctl status wazuh-agent`),
  - dashboard evidence (active endpoint + incoming events).

### Security/Engineering Takeaways

- "Agent running" is not enough; you need dashboard-side data path validation.
- Early ingestion checks reduce false confidence before detections are added.

### Next Steps

- Onboard router and Kali logs.
- Define normalized field mapping checklist.
- Build first practical SOC dashboard view and triage workflow notes.
