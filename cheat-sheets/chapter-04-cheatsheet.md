## Chapter 4 Cheat Sheet: VMkernel Adapters, NIC Teaming, NIOC

### VMkernel Traffic Types
| Service | Purpose |
|---|---|
| Management | Host-to-vCenter, ESXCLI/API |
| vMotion | Live migration of compute state |
| Provisioning | Cold migration, cloning, snapshot ops (uses NFC) |
| Fault Tolerance logging | FT primary/secondary VM state sync |
| vSAN | vSAN cluster data/metadata traffic |
| NFC | Network File Copy (datastore file ops) |
| vSphere Replication / NFC | Replication traffic for VR |

### NIC Teaming Load Balancing Policies
| Policy | Physical Switch Config | Available On |
|---|---|---|
| Route based on originating virtual port ID | None (default) | vSS + vDS |
| Route based on IP hash | Static EtherChannel (802.3ad static) | vSS + vDS |
| Route based on source MAC hash | None | vSS + vDS |
| Route based on physical NIC load (LBT) | None | vDS ONLY |
| Use explicit failover order | None | vSS + vDS |

**LBT trigger:** rebalance when uplink utilization > 75% sustained over 30-second interval.

### Failover Order States
- **Active** — carries traffic normally
- **Standby** — used only on failure of all active uplinks
- **Unused** — never carries traffic for this portgroup/traffic type

### Network I/O Control (NIOC v3)
- **Shares:** Low=25, Normal=50, High=100, Custom 1-100 — govern contention only.
- **Reservations:** guaranteed minimum bandwidth per traffic type. Sum of all reservations ≤ 75% of bandwidth of the LEAST-capable physical adapter on the switch.
- **Limits:** hard cap on bandwidth for a traffic type, regardless of availability.

### Jumbo Frames
- MTU = 9000 (default 1500).
- Must configure at THREE layers: vSwitch/portgroup, VMkernel adapter, physical switch ports.
- Command: `esxcli network nic set -n vmnicX -M 9000` / `esxcli network ip interface set -i vmkX -m 9000`

### Multi-NIC vMotion
- Create 2+ VMkernel adapters tagged for vMotion.
- Each adapter: one uplink Active, others Standby — pattern reversed per adapter so all uplinks are used in parallel.

### TCP/IP Stacks
| Stack | Use Case |
|---|---|
| Default | Management, general host traffic |
| vMotion | Isolated routing/gateway for vMotion, supports routed vMotion |
| Provisioning | Isolated routing/gateway for cold migration, cloning, NFC |

### Common Exam Traps
- Choosing IP hash without configuring static EtherChannel → connectivity loss.
- Confusing LACP (dynamic LAG) with IP hash (static) — not interchangeable.
- Forgetting reservation quota (75% rule) when stacking multiple traffic-type reservations.
- Setting jumbo frames on only one layer (VMkernel only, or switch only).
