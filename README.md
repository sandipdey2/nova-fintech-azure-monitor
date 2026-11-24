# Nova FinTech – Monitor and Maintain Azure Resources

**Final Submission Package**  
**Author:** Sandip Dey  
**Date:** November 2026  

Complete evidence package for the Udacity project covering Azure Backup, Azure Site Recovery, Azure Monitor, Log Analytics, incident investigation, and recovery workflows.

## Project Overview

Nova FinTech is a digital banking startup requiring strong backup, monitoring, and disaster recovery for its production web application VM.

| Item | Value |
|------|-------|
| Resource Group | `nova-fintech-rg` |
| Primary Region | East US 2 |
| Secondary Region (ASR) | Central US |
| Recovery Services Vault (Backup) | `nova-rsv` |
| Recovery Services Vault (ASR) | `nova-rsv-dr` |
| Protected VM | `nova-web-vm` |
| Restored VM | `nova-webr-nova-web-vm` |

## Repository Structure

```
.
├── docs/                                      # Written documentation
│   ├── Part1-Backup-and-ASR.md
│   ├── Part1-ASR.docx
│   ├── Part2-Monitoring-and-Alerting.md
│   ├── Part2-Monitoring-DR.docx
│   ├── Part2-TestFailover.docx
│   ├── Part3-Incident-Investigation.md
│   ├── Part3-Monitoring.docx
│   ├── Part4-Recovery-and-Restoration.md
│   ├── Part4-Recovery.docx
│   └── Screenshot-Checklist.md
├── screenshots/
│   ├── Part1/                                 # Backup & ASR evidence
│   ├── Part2/                                 # Monitoring & alerting evidence
│   ├── Part3/                                 # Incident investigation evidence
│   └── Part4/                                 # Recovery & restoration evidence
└── README.md
```

## Submission Checklist

### Part 1 – Backup & Disaster Recovery
- [x] Backup policy (daily, 30-day retention)
- [x] VM protected by Azure Backup
- [x] Successful backup job
- [x] ASR replication Protected / Healthy
- [x] Network mapping completed
- [x] Successful Test Failover + Cleanup

### Part 2 – Threat Monitoring & Detection
- [x] Log Analytics workspace (`nova-law-monitor`)
- [x] VM Insights enabled
- [x] Diagnostic settings streaming metrics
- [x] Alert rule (CPU > 80% for 5 min, Severity 2)
- [x] Action group with email notification
- [x] Triggered alert evidence (email + portal)

### Part 3 – Simulated Incident
- [x] PowerShell CPU load executed
- [x] Data Collection Rule with Performance Counters
- [x] Heartbeat confirmed in Log Analytics
- [x] KQL query + results showing CPU data
- [x] VM Insights CPU chart

### Part 4 – Recovery & Restoration
- [x] Original VM stopped (deallocated)
- [x] Most recent recovery point selected
- [x] Alternate-location restore to new VM
- [x] Restore job Completed
- [x] Restored VM running in same VNet/subnet
- [x] ASR test failover validated

## Key Evidence Summary

| Part | Status | Primary Evidence |
|------|--------|------------------|
| Part 1 | **PASS** | Backup jobs Succeeded, ASR Healthy, Test Failover Succeeded |
| Part 2 | **PASS** | CPU alert fired (email + portal), Log Analytics + diagnostics |
| Part 3 | **PASS** | DCR + Perf counters, KQL results, VM Insights chart |
| Part 4 | **PASS** | Deallocated → Restore Completed → Restored VM Running |

## Notes

- All resources use the required tags where policy is enforced: `department=Engineering environment=Dev`
- Network Watcher may be blocked by lab policy; alternative CLI and Portal evidence is provided

