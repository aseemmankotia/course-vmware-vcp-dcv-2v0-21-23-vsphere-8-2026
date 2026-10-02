# vSAN & SPBM Cheat Sheet

## Cluster Basics
| Item | Value |
|---|---|
| Min hosts (standard cluster) | 3 |
| Two-node cluster | 2 data hosts + 1 witness |
| Max hosts per cluster | 64 |
| Witness role | Holds witness components only, no VM data |

## OSA Disk Groups
| Tier | Device | Role |
|---|---|---|
| Cache | SSD/flash only | Hybrid: read cache + write buffer; All-flash: write buffer only |
| Capacity | HDD (hybrid) or SSD/NVMe (all-flash) | Stores actual VM data |

Max 5 disk groups/host, max 7 capacity devices per disk group (OSA).

## ESA vs OSA
| Feature | OSA | ESA |
|---|---|---|
| Disk groups | Yes (cache+capacity) | No — single storage pool/host |
| Device type | Hybrid or all-flash | All-flash NVMe only |
| Erasure coding efficiency | Higher overhead | Native, lower overhead |
| Filesystem | vSAN FS | Log-structured FS |

## FTT / RAID Matrix
| FTT | RAID Type | Min Hosts | Capacity Overhead |
|---|---|---|---|
| 1 | RAID-1 (Mirror) | 3 | 2x |
| 1 | RAID-5 (Erasure) | 4 | 1.33x |
| 2 | RAID-1 (Mirror) | 5 | 3x |
| 2 | RAID-6 (Erasure) | 6 | 1.5x |
| 3 | RAID-1 (Mirror only) | 7 | 4x |

**Rule:** RAID-5 = FTT1 only. RAID-6 = FTT2 only. Erasure coding always cheaper on capacity but higher write amplification/CPU vs mirroring.

## SPBM Workflow
1. Define policy (FTT, RAID type, IOPS limit, checksum).
2. Assign policy to VM/VMDK at deploy or edit-settings time.
3. vSAN places components to satisfy policy (may trigger resync).

## vSAN Health & Resync
- Health Service monitors: network, physical disk, data, cluster, capacity, limits.
- Object Repair Timer default: **60 minutes** before resyncing absent components.
- Resync types: policy compliance change, host maintenance mode, absent component timeout.

## vVols Architecture
| Component | Purpose |
|---|---|
| Storage Container | Array-side capacity pool (replaces datastore) |
| Protocol Endpoint (PE) | I/O access/multiplexing point to array |
| VASA Provider | Control plane; exposes array capabilities to vCenter |
| Config vVol | VM home files (.vmx, logs) |
| Data vVol | Per-VMDK object |
| Swap vVol | VM swap file |
| Memory vVol | Optional, for snapshots with memory state |

**Key exam distinction:** vVols = per-VM array data services. VMFS/NFS = per-datastore/LUN granularity only.

## Stretched Cluster
- 2 data fault domains (Preferred + Secondary) + 1 Witness site.
- RTT ≤5ms between data sites (synchronous writes).
- Witness RTT tolerance is higher/looser than data-site RTT — exam differentiates these two numbers.

## Common Exam Traps
- Confusing FTT number with RAID type support (RAID-5 can't do FTT=2).
- Assuming ESA still uses disk groups — it does not.
- Thinking vVols eliminates the need for a VASA provider — it's mandatory.
- Applying stretched-cluster witness RTT rule to data-site RTT (they differ).
