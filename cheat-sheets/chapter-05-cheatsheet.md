## Chapter 5: Datastores, Adapters & Multipathing Cheat Sheet

### VMFS Versions
| Feature | VMFS5 | VMFS6 |
|---|---|---|
| Block size | 1MB (fixed) | 1MB (fixed) |
| UNMAP | Manual (esxcli) | Automatic (async, default priority Low) |
| 512e support | Yes | Yes |
| 4Kn support | No | Yes |
| Partition table | GPT | GPT |

### NFS Versions
| Feature | NFS 3 | NFS 4.1 |
|---|---|---|
| Auth | AUTH_SYS (host trust) | AUTH_SYS or Kerberos (krb5/krb5i) |
| Multipathing | No (network teaming only) | Yes (session trunking) |
| Kerberos | Not supported | Supported |

### Storage Adapter Types
| Type | CPU Offload | Notes |
|---|---|---|
| Software iSCSI | None | Uses VMkernel + host CPU |
| Dependent HW iSCSI | Partial | Relies on ESXi network config |
| Independent HW iSCSI | Full | Fully self-contained adapter |
| FC HBA | Full (protocol-specific) | Dedicated Fibre Channel fabric |
| NVMe-oF | Varies by transport | FC, RDMA (RoCE v2), or TCP |

### iSCSI Discovery & Auth
- **Dynamic (SendTargets):** queries array, auto-returns all targets
- **Static:** manual IQN + IP entry, no query
- **CHAP one-way:** initiator authenticates to target only
- **CHAP mutual:** both sides authenticate each other

### NMP Architecture
- **NMP = SATP + PSP**
- **SATP:** array-specific tasks (failover detection/handling)
- **PSP:** determines path used for I/O

### Path Selection Policies
| PSP | Behavior | Failback |
|---|---|---|
| Fixed | Uses designated preferred path | Auto fails back when preferred path restored |
| MRU | Uses last active path, no preferred path | No failback — stays on current path |
| Round Robin | Cycles across all active paths (default: 1000 IOPS or 10MB per path) | N/A — continuous rotation |

### RDM Compatibility Modes
| Mode | SCSI Command Pass-through | Snapshots | Use Case |
|---|---|---|---|
| Physical (pRDM) | Nearly full | No | Cross-host WSFC, SCSI-3 reservations |
| Virtual (vRDM) | Virtualized | Yes | General raw disk with vSphere feature support |

### Exam Gotchas
- VMFS6 UNMAP is automatic; VMFS5 requires manual `esxcli storage vmfs unmap`.
- Only NFS 4.1 supports Kerberos — NFS 3 is host-trust only (AUTH_SYS).
- CHAP is iSCSI-specific; Kerberos is NFS-specific — do not mix them up.
- Fixed PSP fails back automatically; MRU does not.
- Round Robin default switch threshold is 1000 IOPS, not IOPS=1 or unlimited.
- pRDM cannot be used with snapshots; use vRDM if snapshot support is required.
- Independent hardware iSCSI adapters offload the most CPU work; software iSCSI offloads none.
