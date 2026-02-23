# Lab Architecture

## Design Goals

- Simulate a small corporate environment with realistic segmentation.
- Centralize logs for detection and triage workflows.
- Enforce HITL approval before high-impact response actions.
- Keep the lab stable on a resource-constrained host.

## Proposed Environment

- Hypervisor: VMware Fusion
- Host: Apple Silicon MacBook Pro (M3 Pro, 18 GB RAM)
- 1 Kali ARM endpoint (`lab-attk-01`)
- 1 Ubuntu ARM server (`lab-srv-01`)
- 1 Ubuntu ARM router VM (`lab-rtr-01`)
- 1 Ubuntu ARM SIEM VM (`lab-siem-01`)
- Segmented virtual networks

## Current Implemented Environment (as of 2026-02-22)

- Router-enabled segmentation is operational between:
  - `corp`: `10.10.10.0/24`
  - `server`: `10.10.20.0/24`
- Wazuh all-in-one server deployed on `lab-siem-01`.
- Wazuh dashboard reachable internally via the SIEM server address.
- First endpoint agent enrolled: Ubuntu server (`lab-srv-01`, `10.10.20.10`).
- Basic ingestion validated in Wazuh Threat Hunting and Endpoints views.

## Data Flow (Current + Planned)

1. Endpoints/servers generate logs (Linux logs now).
2. Wazuh agents forward endpoint events to Wazuh manager/indexer.
3. Wazuh dashboard enables hunting + endpoint health validation.
4. Detection rules generate alerts.
5. AI assistant drafts summaries/recommendations.
6. Human analyst reviews and approves/rejects actions.
7. Decision and rationale are logged for auditability.

## Near-Term Architecture Gaps

- Router and Kali telemetry are not yet onboarded.
- Field normalization conventions are not yet documented and enforced.
- SOC dashboard views (triage queue, auth anomalies, endpoint health) are still pending.

## Human-in-the-Loop Control Points

Human approval required for:

- Severity escalation changes
- Host isolation actions
- Block/deny rule deployment

## Security/Operational Assumptions

- Isolated lab only (no production systems)
- Least privilege admin model where possible
- All tests are controlled and documented

## Platform and Expansion Notes

- Proxmox remains a valid future path if a dedicated bare-metal host is added.
- Current architecture decisions are platform-agnostic.
