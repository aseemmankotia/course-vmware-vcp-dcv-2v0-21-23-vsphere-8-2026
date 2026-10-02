## vSS vs vDS — Quick Comparison

| Feature | vSS | vDS |
|---|---|---|
| Configuration scope | Per-host, independent | Centralized via vCenter, spans hosts |
| Requires vCenter | No | Yes |
| NIOC (shares/reservations/limits) | No | Yes |
| LACP (dynamic LAG) | No | Yes |
| Private VLANs (PVLAN) | No | Yes |
| Load Based Teaming (LBT) | No | Yes |
| Port mirroring, NetFlow, LLDP/CDP (both directions) | No | Yes |
| Rollback / Network Health Check | No | Yes |

## VLAN Tagging Modes

| Mode | VLAN ID on Port Group | Tag added/stripped by | Physical switch port |
|---|---|---|---|
| EST (External Switch Tagging) | 0 | Physical switch | Access port |
| VST (Virtual Switch Tagging) | 1–4094 (single VLAN) | ESXi vSwitch/port group | Trunk port |
| VGT (Virtual Guest Tagging) | 4095 | Guest OS (802.1Q driver) | Trunk port |

**Exam trap:** VLAN ID 4095 does NOT mean "no VLAN" — it means pass-all/VGT. VLAN ID 0 means EST/no tagging at vSwitch.

## Private VLANs (PVLAN)

| Secondary Type | Can talk to |
|---|---|
| Promiscuous | All ports (Isolated, Community, Promiscuous) |
| Community | Same Community + Promiscuous |
| Isolated | Promiscuous only |

PVLANs require a Primary VLAN plus one or more Secondary VLANs configured at the vDS level, then assigned to port groups. Physical switch must support PVLAN or trunk all secondary VLAN IDs.

## Uplinks & Teaming (vDS)

| Policy | Active/Active? | Physical switch config needed |
|---|---|---|
| Route based on originating virtual port | Static pinning | None |
| Route based on IP hash | Yes | Static EtherChannel/LAG required |
| Route based on physical NIC load (LBT) | Yes, dynamic | None |
| Use explicit failover order | No (active/standby) | None |
| LACP (dynamic LAG) | Yes | LACP-enabled ports required |

## vDS Versions & Compatibility

- Higher vDS version unlocks newer features but raises minimum required ESXi host version.
- Example: vDS 8.0.0 requires ESXi 8.0 minimum; vDS 7.0.3 supports ESXi 7.0 U3+ hosts.
- Mixed-version clusters: choose the vDS version matching your OLDEST host that still needs required features.

## Migration vSS → vDS (Zero Downtime)

1. Create vDS + matching distributed port groups (same VLAN config).
2. Add hosts to vDS, assign uplinks.
3. Use **Migrate VMs to Another Network** (or Add and Manage Hosts wizard) to move VM vNICs — VMs stay powered on.
4. Migrate VMkernel adapters (mgmt, vMotion, vSAN) last, one host at a time, to avoid isolation.
5. Remove vSS once all uplinks/VMs are migrated.
