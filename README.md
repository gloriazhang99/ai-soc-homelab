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

## Current Scope (Week 1)

- Documentation baseline
- Lab architecture and network design
- Environment planning (hypervisor, VM specs, segmentation)

## Planned Stack

- Hypervisor: Proxmox (preferred) or VirtualBox
- Endpoints: Windows Server + Windows clients + Linux server
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

- Branch: `codex/bootstrap`
- Week: 1
- Progress: Documentation and environment planning in progress
