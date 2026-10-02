# Chapter 2 Cheat Sheet: vCenter Server Deployment & Inventory Design

## VCSA Deployment Sizes (vSphere 8 Config Max)
| Size | Max Hosts | Max VMs |
|---|---|---|
| Tiny | 10 | 100 |
| Small | 100 | 1,000 |
| Medium | 400 | 4,000 |
| Large | 1,000 | 10,000 |
| X-Large | 2,000 | 35,000 |

**Exam trap:** Choosing an oversized appliance wastes resources; choosing undersized causes management failures at scale. Match size to actual host/VM count, not future guesses.

## Deployment Stages
- **Stage 1 (OVA deploy):** target host/vCenter, appliance name, root password, deployment size, storage size, network settings.
- **Stage 2 (Configure):** NTP/time sync, SSO domain (new or join existing), enable/disable SSH, CEIP.

## PSC Architecture (Legacy Context)
| Model | Status |
|---|---|
| External PSC | Deprecated, removed as of vSphere 7.0 — not deployable for new installs |
| Embedded PSC | Current and only supported model since 7.0 |

**Exam trap:** Questions may reference legacy external PSC topologies (6.x) to test whether you know it's obsolete — pick embedded/converged answers.

## Enhanced Linked Mode (ELM)
- Links multiple vCenter Server instances into a single inventory view.
- Requirement: **same SSO domain** across all linked instances.
- Max: **15 vCenter Server instances** per SSO domain (vSphere 8).
- No external PSC needed — embedded architecture handles data replication.

## Inventory Hierarchy
| Object | Purpose |
|---|---|
| Datacenter | Top-level container for hosts, clusters, VMs, datastores, networks |
| Cluster | Groups hosts for DRS/HA/vSAN |
| Folder | Organizes objects for permissions/structure (VM, host, datastore, network folders) |
| Resource Pool | Allocates CPU/memory shares, reservations, limits — NOT storage/network |
| Host | Physical ESXi server |
| VM | Virtual machine object |

## vCenter High Availability (vCenter HA)
- 3-node cluster: **Active, Passive, Witness**.
- Protects against appliance/host failure with automated failover.
- Requires a dedicated HA network for node replication/heartbeat.
- Distinct from vSphere HA (protects VMs at cluster level, not appliance-specific state).

## Backup & Restore
- **File-based backup:** via VAMI (port 5480) or API; targets FTP(S), HTTP(S), SFTP, NFS, SMB.
- Captures config, inventory, embedded PostgreSQL DB — **not** a full VM image.
- Restore performed via the VCSA installer's Restore workflow (deploys new appliance, restores data).
- Image-based (VM-level) backup requires separate backup software (e.g., snapshot-based tools).

## SSO Domains & Identity Sources
- Default SSO domain: **vsphere.local**.
- Identity sources: Active Directory (over LDAPS), OpenLDAP, local OS accounts.
- ELM requires shared SSO domain; separate SSO domains = separate, unlinked inventories (unless using Hybrid Linked Mode for cloud scenarios).
