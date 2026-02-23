# ai-soc-homelab (Human-in-the-Loop)

## Objective

Build a realistic cybersecurity home lab that mirrors corporate SOC workflows:

- Detection engineering
- Incident triage and response
- Automation with human approval gates
- Measurable outcomes (MTTD/MTTR)

## Why This Project

This project is designed for:

- Practical skill growth for cybersecurity roles
- Hands-on Human-in-the-Loop (HITL) AI security operations

## Current Scope (Weeks 1-2)

- Documentation baseline and architecture
- Segmented network implementation (`corp` + `server`)
- SIEM foundation deployment (Wazuh server + first enrolled agent)

## Planned Stack

- Hypervisor: VMware Fusion (current on M3 Pro); Proxmox possible on future dedicated host
- Endpoints (phased): Linux server + Kali now; Windows client/Server later as host resources allow
- Security tooling: Wazuh/Elastic, Sysmon, Suricata/Zeek
- ATT&CK-aligned detections and playbooks
- HITL AI assistant for triage support (approval required for high-impact actions)

## High Level Plan

1. Environment setup and segmentation
2. Telemetry and SIEM onboarding
3. Detection engineering (Sigma/KQL)
4. Incident response playbooks and case workflow
5. HITL AI automation and audit logging
6. Adversary simulation and metrics reporting

## Repo Structure

- `/docs` architecture + learning notes
- `/lab` environment and host configs
- `/detections` detection content
- `/playbooks` response procedures
- `/incidents` case records
- `/automation` HITL AI scripts and policy
- `/metrics` SOC performance tracking

## Status

- Branch: `codex/week2-siem-pipeline`
- Week: 2
- Progress: Routing baseline complete; Wazuh server and first Ubuntu agent validated with basic ingestion

## Immediate Next Milestones

1. Onboard additional telemetry sources (router logs and Kali logs).
2. Normalize key fields for triage consistency (host, src/dst IP, user, action, severity).
3. Build a first SOC dashboard view for daily monitoring + incident handoff.
4. Add sanitized implementation evidence (screenshots/diagram) with secrets/IP exposure review.
