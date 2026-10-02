## VM Creation, Templates & Content Libraries — Cheat Sheet

### Hardware Version → ESXi Release
| ESXi Version | Hardware Version |
|---|---|
| 6.0 | 11 |
| 6.5 | 13 |
| 6.7 | 14 |
| 7.0 GA | 17 |
| 7.0 U2 | 19 |
| 8.0 GA | 20 |
| 8.0 U2 | 21 |

**Rule:** A VM's hardware version must be ≤ the max supported version of the target ESXi host. Deploying/importing a newer HW version onto older hosts is blocked or warned.

### Convert vs Clone to Template
| Action | Source VM After | Use When |
|---|---|---|
| Convert to Template | Gone (becomes template, non-runnable) | You don't need the original VM anymore |
| Clone to Template | Stays running/unchanged | Source must remain in production |

**Requirement:** VM must be powered off to Convert to Template or Export OVF.

### Content Library Types
| Type | Description |
|---|---|
| Local | Source of truth; created/managed in current vCenter; can be published |
| Published | A local library shared via URL for others to subscribe to |
| Subscribed | Points to a published library's URL; pulls a synced copy |

**Sync modes (subscribed only):**
- **Immediate** — downloads all content now
- **On-demand** — metadata only; content pulled when deployed (saves storage/bandwidth)

### OVF vs OVA
| Format | Structure | Notes |
|---|---|---|
| OVF | Multiple files (.ovf, .vmdk, .mf) | Files must stay together in one folder |
| OVA | Single tar archive | Easiest to transport as one file |

**Export/Import:** Both work across vCenter instances without shared SSO — useful for cross-org or air-gapped transfers.

### Customization Specification
- Applied during template/clone deployment.
- Personalizes hostname, SID (Windows via Sysprep), IP config, domain join, license key.
- Stored in vCenter; exportable/importable as XML.
- Not the same as OVF properties (vApp parameters).

### Linked Clone vs Full Clone (Horizon/VDI context)
| Type | Storage | Speed | Dependency |
|---|---|---|---|
| Linked Clone | Low (shares base/replica disk + delta disk) | Fast provisioning | Depends on parent/replica |
| Full Clone | High (independent full copy) | Slower provisioning | Fully independent |

### Common Exam Traps
- Templates cannot be powered on — must deploy a new VM first.
- Convert to Template removes the original VM; Clone to Template does not.
- Importing higher HW version OVF onto lower-capability hosts fails/warns — no silent auto-downgrade.
- On-demand sync ≠ no sync — metadata still syncs immediately, only content download is deferred.
