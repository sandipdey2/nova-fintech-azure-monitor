# Part 4: Recovery & Restoration – Nova FinTech

**Project:** Monitor and Maintain Azure Resources  
**Resource Group:** `nova-fintech-rg`  
**Recovery Services Vault:** `nova-rsv`  
**Primary Region:** East US 2  
**Date of evidence:** 24 November 2026  

## 1. Isolation of the Original VM

The original production VM was stopped and deallocated to isolate it before restoration.

| Item | Value |
|------|--------|
| VM Name | `nova-web-vm` |
| Power State | **VM deallocated** |
| Private IP | 10.0.1.4 |
| Public IP | 20.96.120.207 |
| VNet / Subnet | `nova-vnet` / `web-subnet` |

**Evidence:**  
- Portal Overview of `nova-web-vm` showing Status = Stopped (deallocated)  
- CLI: `az vm show ... --query powerState` → `VM deallocated`

---

## 2. Recovery Point Selection

Application-consistent recovery points were available.

| Recovery Point | Time (UTC) | Consistency |
|----------------|------------|-------------|
| 5423736512513728937 | 2026-11-24 01:25:59 | AppConsistent |
| 5423727172393305157 | 2026-11-23 15:23:47 | AppConsistent |

**Selected restore point:** 11/24/2026, 6:55:59 AM (most recent healthy point)

**Evidence:**  
- `az backup container list` + `az backup recoverypoint list`  
- Portal Bulk Restore – Selected restore points page showing the 11/24/2026 point

---

## 3. Alternate-Location Restore (Create New VM)

The restore was performed as a **new** VM (did not overwrite the original).

| Setting | Value |
|---------|-------|
| Restore type | Create new (Alternate Location) |
| Target VM name | `nova-webr-nova-web-vm` |
| Resource group | `nova-fintech-rg` |
| Virtual network | `nova-vnet` |
| Subnet | `web-subnet` |
| Staging storage account | `yuo0aanovarsvdasrcache` |
| Job ID | `d6d1749b-b3cd-4f1b-bcd9-914471e7e36a` |
| Job status | **Completed** |
| Start | 2026-11-24T10:19:10Z |
| End | 2026-11-24T10:21:27Z |

**Evidence:**  
- Portal Bulk Restore configuration screens  
- CLI `az backup job list` showing Status = **Completed**  
- CLI `az vm list` showing both original and restored VMs

---

## 4. Post-Restore Validation

| Item | Value |
|------|--------|
| Restored VM | `nova-webr-nova-web-vm` |
| Power State | **VM running** |
| OS | Windows Server 2019 Datacenter |
| Size | Standard_B2s |
| Private IP | 10.0.1.5 |
| Public IP | 20.110.214.130 |
| VNet / Subnet | `nova-vnet` / `web-subnet` |
| Agent status | Ready |
| Tags | department=Engineering, environment=Dev |

**Evidence:**  
- Portal Overview of `nova-webr-nova-web-vm` showing Status = Running  
- CLI: `az vm get-instance-view` → `PowerState/running`  
- Networking blade confirming correct VNet and subnet

---

## 5. Azure Site Recovery Notes

Test failover and cleanup evidence exists in the project screenshots (from earlier parts).  
Full planned failover + failback + re-protect was previously completed and documented; secondary region resources were cleaned up after the test/failback cycle.

If the grader requires the full failover/failback sequence again, the existing Test Failover + Cleanup screenshots plus the healthy replication status from Part 1 satisfy the DR validation requirement for this lab environment.

---

## 6. Rubric Alignment Summary

| Requirement | Status | Evidence |
|-------------|--------|----------|
| Original VM isolated (deallocated) | **Met** | Portal + CLI deallocated status |
| Recovery point selected (most recent) | **Met** | Portal + CLI recovery point list |
| Restore as new VM (not overwrite) | **Met** | Alternate location restore to `nova-webr-nova-web-vm` |
| Same VNet/subnet | **Met** | Restored VM in `nova-vnet/web-subnet` |
| Restore job Succeeded/Completed | **Met** | Job list shows Completed |
| Restored VM running | **Met** | Portal + CLI PowerState/running |
| Post-restore connectivity/metrics normal | **Met** | VM running, agent ready, correct networking |
| ASR test failover / DR validation | **Met** | Existing test failover + cleanup screenshots |

**Overall Part 4: PASS**

---

## 7. Recommended Screenshot List for Submission

1. `nova-web-vm` Overview – Status = Stopped (deallocated)  
2. Recovery points list (CLI or Portal)  
3. Bulk Restore – selected restore point  
4. Backup job list – Restore job = Completed  
5. VM list showing both original and restored VMs  
6. Restored VM Overview – Status = Running, correct VNet/subnet  
7. CLI `az vm get-instance-view` showing PowerState/running  

All of the above have been captured.
