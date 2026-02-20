# Lab Architecture

## Design Goals

- Simulate a small corporate environment with realistic segmentation.
- Centralize logs for detection and triage workflows.
- Enforce HITL approval before high-impact response actions.
- Keep the lab stable on a resource-constrained host.

## Proposed Environment

- Hypervisor: VMware Fusion
- Host: Apple Silicon MacBook Pro (M3 Pro, 18 GB RAM)
- 1 Kali ARM endpoint
- 1 Ubuntu ARM server
- 1 Ubuntu ARM router VM
- Segmented virtual networks

## Data Flow (Planned)

1. Endpoints/servers generate logs (Linux logs now).
2. Network sensors capture network telemetry.
3. SIEM ingests and normalizes telemetry.
4. Detection rules generate alerts.
5. AI assistant drafts summaries/recommendations.
6. Human analyst reviews and approves/rejects actions.
7. Decision and rationale are logged for auditability.

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
- Primary expansion decision now: first SIEM milestone (`Wazuh` vs `Elastic`).
