# Part 1: Backup & Disaster Recovery Implementation

## Recovery Services Vault
Created in the same region as the primary VM (`eastus2`).

## Azure Backup
- **Policy name:** Daily-30Day-Policy
- **Schedule:** Daily at 02:00 UTC
- **Retention:** 30 days
- **Protected VM:** nova-web-vm

### Evidence Required
- Backup policy blade (schedule + retention)
- VM listed under Protected items
- Backup job with status **Succeeded**
- Test restore / restore validation job **Succeeded**

## Azure Site Recovery
- **Source region:** East US 2
- **Target region:** Central US
- **Replication policy:** Default or custom RPO
- **Network mapping:** Primary VNet ↔ Secondary VNet

### Evidence Required
- Replication status: **Protected / Healthy**
- Network mapping configuration
- Test Failover job with status **Succeeded**

## Screenshot Naming
```
part1_backup_policy.png
part1_vm_protected.png
part1_backup_job_succeeded.png
part1_restore_validation.png
part1_asr_replication_healthy.png
part1_network_mapping.png
part1_test_failover_succeeded.png
```
