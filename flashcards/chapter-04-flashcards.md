## Chapter 4: VMkernel Adapters, NIC Teaming, and Network I/O Control — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | NIOC reservation admission-control rule? | Sum of all system traffic reservations cannot exceed 75% of the bandwidth of the physical adapter with the LEAST capacity on the switch. Exam tip: applies to NIOC v3 reservations, not shares. |
| 2 | Jumbo frame MTU value used for vMotion/vSAN performance tuning? | 9000 (vs default 1500). Exam tip: must be set consistently on vSwitch/portgroup, VMkernel adapter, AND physical switch ports. |
| 3 | Load Based Teaming (LBT) rebalance trigger? | Uplink utilization exceeding 75% sustained over a 30-second sampling interval. Exam tip: LBT is available only on vSphere Distributed Switch, never on a standard switch. |
| 4 | NIC teaming failover order states? | Active, Standby, Unused. Exam tip: Unused uplinks never carry traffic even during failover — a common wrong-answer trap. |
| 5 | Route based on IP hash — physical switch requirement? | Requires static EtherChannel (802.3ad static link aggregation) on the physical switch. Exam tip: LACP (dynamic) is NOT compatible with IP hash teaming policy directly — LACP uses its own separate LAG configuration on vDS. |
| 6 | List the VMkernel traffic service types tested on the exam. | Management, vMotion, Provisioning, Fault Tolerance logging, vSAN, NFC, vSphere Replication, vSphere Replication NFC. Exam tip: each is an individual checkbox on a VMkernel adapter, and one adapter can support multiple services. |
| 7 | Multi-NIC vMotion configuration pattern? | Create 2+ VMkernel adapters for vMotion, each with a DIFFERENT uplink set to Active and the rest set to Standby (opposite pattern per adapter). Exam tip: this parallelizes vMotion across multiple physical NICs to speed host evacuation. |
| 8 | NIOC share values: Low / Normal / High? | Low = 25, Normal = 50, High = 100 (custom values 1–100 also allowed). Exam tip: shares only matter when there's contention for bandwidth; they don't guarantee bandwidth like reservations do. |
| 9 | What distinguishes the default, vMotion, and Provisioning TCP/IP stacks? | Each maintains its own independent routing table, default gateway, and DNS settings. Exam tip: use the vMotion/Provisioning stack when that traffic must be routed over a different gateway than the management network. |
| 10 | Default NIC teaming policy on a new standard vSwitch or portgroup? | Route based on originating virtual port ID. Exam tip: requires NO special physical switch configuration, unlike IP hash. |
| 11 | Which NIC teaming load balancing policy is exclusive to vSphere Distributed Switch? | Route based on physical NIC load (Load Based Teaming / LBT). Exam tip: standard switches only offer Port ID, IP hash, source MAC hash, and explicit failover order. |
| 12 | ESXCLI command to set jumbo frames (MTU 9000) on a physical NIC/VMkernel port? | esxcli network nic set -n vmnicX -M 9000 (physical NIC) and esxcli network ip interface set -i vmkX -m 9000 (VMkernel port). Exam tip: also verify at the vSwitch/portgroup MTU setting in the UI. |
