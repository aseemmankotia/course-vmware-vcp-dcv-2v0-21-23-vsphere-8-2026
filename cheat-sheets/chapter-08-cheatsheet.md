# Chapter 8 Cheat Sheet: Snapshots, Clones, vMotion/Storage vMotion

## Snapshot File Architecture
| File | Purpose |
|---|---|
| `.vmdk` (base disk) | Original disk, becomes read-only once snapshot taken |
| `-delta.vmdk` | Growable file capturing all writes after snapshot; merged back on delete (consolidation) |
| `.vmsd` | Snapshot metadata/hierarchy (always created) |
| `.vmsn` | Memory state — only created if 'Snapshot the VM's memory' option selected |

**Consolidation:** merges delta disk(s) back into base disk when snapshot deleted. 'Needs consolidation' warning = leftover delta files from a failed/interrupted merge.

**Snapshot sprawl causes:** backup software not cleaning up snapshots, forgotten manual snapshots, failed consolidation jobs, insufficient datastore space blocking merge.

**Limits:** Max 32 snapshots per chain. Best practice: ≤2-3 snapshots, remove within 24-72 hours (performance degrades as chain grows).

## Full Clone vs Linked Clone
| Feature | Full Clone | Linked Clone |
|---|---|---|
| Independence | Fully independent | Depends on parent base disk |
| Storage use | Full disk size | Only delta (much smaller) |
| Parent deletion impact | None | Breaks the clone |
| Typical use | Isolated test/prod VMs | VDI, rapid provisioning |

## vMotion Prerequisites (Standard, compute-only)
- Shared storage visible to source AND destination hosts
- Compatible CPUs (same vendor) OR EVC baseline masking feature differences
- vMotion-enabled VMkernel adapter on both hosts
- Minimum network bandwidth: 250 Mbps (10 Gbps recommended for multi-NIC vMotion)
- VM not connected to host-local devices (e.g., CD-ROM mapped to local ISO)

## EVC (Enhanced vMotion Compatibility)
- Masks CPU feature sets to the lowest common denominator generation in the cluster
- Baseline is vendor-specific — **cannot mix Intel and AMD hosts** in one EVC cluster
- Set baseline to match the OLDEST CPU generation in the cluster

## Storage vMotion vs Standard vMotion vs vMotion without Shared Storage
| Feature | Standard vMotion | Storage vMotion | vMotion w/o Shared Storage |
|---|---|---|---|
| Moves compute (host) | Yes | No | Yes |
| Moves disk (datastore) | No | Yes | Yes |
| Requires shared storage | Yes | No | No |
| Downtime | Zero | Zero | Zero |
| Use case | Host maintenance/DRS | Datastore rebalancing/upgrade | Migrating between hosts with no shared datastore |

## Exam Traps
- Assuming snapshots block vMotion — they do NOT.
- Mixing Intel/AMD in an EVC cluster — not supported.
- Forgetting the VMkernel adapter needs vMotion traffic type explicitly enabled.
- Confusing Storage vMotion (datastore change only) with vMotion without shared storage (host + datastore change together).
