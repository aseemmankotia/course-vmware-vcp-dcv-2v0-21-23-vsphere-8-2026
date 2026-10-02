## vSphere HA, FT & Admission Control — Cheat Sheet

### HA Cluster Fundamentals
- One **Master** host elected per cluster (via election protocol); all others are **Agent** hosts.
- Master monitors host/VM health, tracks resources, and initiates restarts.
- Heartbeats: Network heartbeats (management network) + **Datastore heartbeats**.
- Default heartbeat datastores: **2** per host; configurable up to **5** via `das.heartbeatDsPerHost`.

### Admission Control Policies
| Policy | How it Works | Key Gotcha |
|---|---|---|
| Cluster Resource Percentage | Reserves % of cluster CPU/Memory for failover; can be automatic or manual | Default computed automatically based on # hosts to tolerate |
| Slot Policy | Slot size = largest CPU reservation + largest memory reservation (defaults 32 MHz/0 MB if none set); # slots = cluster capacity ÷ slot size | One VM with a huge reservation inflates slot size for ALL VMs ("slot fragmentation") |
| Dedicated Failover Host(s) | Up to 4 hosts reserved exclusively for failover; DRS avoids placing VMs there | Wastes capacity if failure never occurs; simplest to reason about |

### Host Isolation Response
- Options: **Power off and restart VMs**, **Shut down and restart VMs**, **Leave powered on** (default in modern releases).
- Isolation detected when host loses network heartbeats AND cannot reach isolation address; datastore heartbeats confirm host is alive but isolated (vs. failed).

### VM Component Protection (VMCP)
- Responds to **APD** (All Paths Down) and **PDL** (Permanent Device Loss).
- PDL response: Power off and restart VMs (default aggressive).
- APD response: Configurable timeout (default 140 sec) before conservative/aggressive restart action.

### VM Restart Priority
- Levels: Lowest, Low, Medium (default), High, Highest, Disabled — order VMs restart post-failure.

### vSphere Fault Tolerance (FT)
| Item | Detail |
|---|---|
| Technology | Fast Checkpointing (modern SMP-FT); vLockstep = legacy single-vCPU tech |
| Max vCPUs | 8 (Enterprise Plus); 2 vCPUs on lower editions |
| Downtime | Zero — live shadow VM takes over instantly on primary failure |
| Snapshots | **Not supported** while FT enabled — must disable FT first |
| Hardware | Requires compatible/EVC-aligned CPUs across hosts; VM hardware version 10+ |
| Unsupported features | Physical RDM, SR-IOV, NPIV, CPU hot-plug, 3D-enabled video, USB passthrough |
| Network | 10 Gbps NIC recommended for FT logging traffic |

### FT vs HA — Quick Comparison
| | HA | FT |
|---|---|---|
| Downtime on failure | Yes (VM restart) | None (instant failover) |
| Data loss | Possible (since last save state) | None |
| Resource overhead | Low (reserved slots/%) | High (duplicate VM running continuously) |
| Use case | General VM availability | Mission-critical, zero-downtime workloads |

### Exam Traps
- Slot policy slot size uses **largest** reservation, not average.
- Default isolation response is **Leave powered on**, not power off.
- FT vCPU limits depend on **license edition**, not just vSphere version.
- Snapshots require **disabling FT first** — common wrong answer is "FT fully supports snapshots."
