# Lab Architecture

## Design Goals

- Simulate small corporate environment
- Centralize logs for detection and triage
- Enforce HITL approval before high-impact response actions

## Proposed Environment

- 1 Hypervisor host (Proxmox or VirtualBox)
- 1 Windows Server (AD/DNS)
- 2 Windows endpoints
- 1 Linux server (app/log source)
- 1 Kali attacker VM
- Segmented virtual networks: `corp`, `server`, `admin`

## Data Flow (Planned)

1. Endpoints/servers generate logs (Sysmon, Windows Event Logs, Linux logs).
2. Network sensors capture network telemetry.
3. SIEM ingests and normalizes telemetry.
4. Detection rules generate alerts.
5. AI assistant drafts summary/recommendations.
6. Human analyst reviews and approves/rejects actions.
7. Decision and rationale logged for auditability.

## Human-in-the-Loop Control Points

Human approval required for:

- Severity escalation changes
- Host isolation actions
- Block/deny rule deployment

## Security/Operational Assumptions

- Isolated lab only (no production systems)
- Least privilege admin model where possible
- All tests are controlled and documented

## Open Decisions

- Hypervisor final choice: Proxmox vs VirtualBox
- SIEM first milestone: Wazuh vs Elastic
- Case management: markdown-only vs TheHive
