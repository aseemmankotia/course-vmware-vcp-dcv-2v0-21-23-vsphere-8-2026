## Chapter 10: vSphere HA, Fault Tolerance, and Admission Control — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Default number of heartbeat datastores per host, and the configurable maximum? | Default: 2. Maximum: 5 (via das.heartbeatDsPerHost). Exam tip: used to distinguish host isolation from host failure. |
| 2 | Maximum vCPUs supported on an FT-protected VM (Enterprise Plus)? | 8 vCPUs. Standard/lower editions limit FT to 2 vCPUs. Exam tip: FT vCPU limit is edition-dependent. |
| 3 | vSphere HA admission control policy that reserves entire hosts for failover? | Dedicated Failover Host(s) policy — up to 4 hosts can be designated; DRS avoids placing VMs on them during normal operation. |
| 4 | What two reservation values determine HA Slot Policy slot size? | The largest CPU reservation and largest memory reservation among powered-on VMs (defaults: 32 MHz CPU / 0 MB memory if unset). Combined = one slot. |
| 5 | vSphere HA isolation response options (3)? | Power off and restart VMs, Shut down and restart VMs, Leave powered on. Default (modern vSphere): Leave powered on. |
| 6 | What mechanism lets HA distinguish an isolated host from a failed host? | Datastore heartbeating — an isolated host still writes heartbeats to designated heartbeat datastores even though network connectivity is lost. |
| 7 | What is VM Component Protection (VMCP) designed to detect? | Storage accessibility failures: APD (All Paths Down) and PDL (Permanent Device Loss). Can trigger VM restart on a healthy host. |
| 8 | Which host in an HA cluster monitors agent hosts and coordinates VM restarts? | The elected Master host. One master is elected per cluster; remaining hosts act as Agent (Slave/Subordinate) hosts. |
| 9 | FT vs HA: which one provides zero-downtime protection with no VM restart? | Fault Tolerance (FT) — keeps a live shadow VM in virtual lockstep (Fast Checkpointing) with zero data loss/downtime. HA restarts the VM after failure, incurring downtime. |
| 10 | Can you take a snapshot of an FT-protected VM while FT is enabled? | No. FT must be temporarily disabled before taking a snapshot, then re-enabled afterward. |
| 11 | What replaced the legacy 'vLockstep' technology in modern multi-vCPU vSphere FT? | Fast Checkpointing — used since vSphere 6.0 for SMP-FT (multi-vCPU support up to 8 vCPUs on Enterprise Plus). vLockstep was limited to single-vCPU FT in older versions. |
| 12 | VM restart priority levels available in vSphere HA? | Lowest, Low, Medium (default), High, Highest, and Disabled — controls the order VMs are restarted after a host failure. |
