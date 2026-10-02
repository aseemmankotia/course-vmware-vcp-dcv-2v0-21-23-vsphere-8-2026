## Chapter 10: vSphere HA, Fault Tolerance, and Admission Control — Practice Questions

**Q1.** A 12-host vSphere HA cluster uses Slot Policy admission control. One VM has a memory reservation of 16 GB and another has a CPU reservation of 4 GHz; no other VMs have reservations. What determines the cluster's slot size?

A) The largest CPU reservation and the largest memory reservation among powered-on VMs, combined into one slot size
B) The average reservation across all powered-on VMs
C) The smallest reservation values to maximize the number of available slots
D) A fixed default slot size of 4 vCPU / 16 GB regardless of VM reservations

<details>
<summary>Answer</summary>

**Correct: A**

HA slot size is calculated from the single largest CPU reservation and the single largest memory reservation found among powered-on VMs in the cluster (using defaults of 32 MHz / 0 MB+overhead if no reservations exist), and these two maximums are combined into one slot size.

**Why the others are wrong:**
- Averaging is not how slot size is calculated; a single large reservation skews all slots.
- Slot size uses the largest, not smallest, reservations — this is a known gotcha causing 'slot fragmentation'.
- There is no fixed 4 vCPU/16GB default; the default per-VM values are 32 MHz CPU and 0 MB memory when no reservation is set.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An administrator configures 4 hosts as Dedicated Failover Hosts in an 8-host cluster. What is the behavior of vSphere HA regarding these hosts during normal operation?

A) DRS load balances VMs onto the failover hosts equally with other hosts
B) vSphere HA and DRS avoid placing VMs on the designated failover hosts unless no other host is available
C) The failover hosts run at 50% capacity to reserve headroom
D) The failover hosts are automatically placed in maintenance mode until a failure occurs

<details>
<summary>Answer</summary>

**Correct: B**

With the Dedicated Failover Hosts policy, HA reserves the specified hosts exclusively for failover; DRS will not place new VMs there during normal operations, keeping capacity free for a failure event.

**Why the others are wrong:**
- DRS specifically excludes these hosts from normal placement — the opposite of load balancing them equally.
- There is no 50% capacity throttling mechanism in this policy.
- Dedicated failover hosts remain powered on and available, not in maintenance mode, so they can instantly host failed-over VMs.

</details>

---

**Q3.** A host loses all management network connectivity but its storage paths remain intact. The cluster is configured with 2 heartbeat datastores. How does vSphere HA determine this is isolation rather than a host failure?

A) The host pings the vCenter Server management IP directly
B) The isolated host powers off automatically to signal isolation
C) The master host observes that the isolated host is still writing heartbeats to the shared heartbeat datastores
D) DRS detects the missing vMotion heartbeat and reports isolation to HA

<details>
<summary>Answer</summary>

**Correct: C**

Datastore heartbeating lets the HA master distinguish an isolated host (still alive, writing to heartbeat datastores) from a genuinely failed host (no heartbeats at all, network or datastore).

**Why the others are wrong:**
- Isolated hosts cannot reach vCenter — that is precisely the condition being detected, not the detection mechanism.
- Isolation response (power off, etc.) happens only after isolation is detected and the isolation response timeout expires — it isn't the detection method itself.
- DRS does not perform isolation detection; this is purely an HA/FDM function.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A cluster stores VMs on an all-flash array using iSCSI. Occasionally, the array experiences an All Paths Down (APD) condition. Which vSphere HA feature is designed to respond to this scenario?

A) Proactive HA
B) vSphere Fault Tolerance
C) VM Component Protection (VMCP)
D) DRS anti-affinity rules

<details>
<summary>Answer</summary>

**Correct: C**

VM Component Protection (VMCP) is the HA feature that detects and responds to datastore accessibility failures — All Paths Down (APD) and Permanent Device Loss (PDL) — by restarting affected VMs on healthy hosts.

**Why the others are wrong:**
- Proactive HA responds to degraded host hardware health (via vendor plugins), not storage path failures.
- Fault Tolerance protects against host failure with a live shadow VM; it does not specifically handle storage APD/PDL events.
- DRS anti-affinity rules control VM placement relative to other VMs, unrelated to storage failures.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** By default, how many heartbeat datastores does vSphere HA select per host, and what is the maximum configurable via das.heartbeatDsPerHost?

A) 1 default, 2 maximum
B) 2 default, 5 maximum
C) 3 default, 8 maximum
D) 5 default, 10 maximum

<details>
<summary>Answer</summary>

**Correct: B**

vSphere HA automatically selects 2 heartbeat datastores per host by default; the advanced option das.heartbeatDsPerHost can be increased up to a maximum of 5.

**Why the others are wrong:**
- 1 default/2 max understates both the default and the ceiling.
- 3 default is incorrect — the default remains 2 regardless of cluster size.
- 5 default overstates the default; 5 is only the maximum, not the default value.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A company wants to deploy a business-critical VM using vSphere Fault Tolerance with 6 vCPUs on vSphere 8 with an Enterprise Plus license. Which statement about this configuration is correct?

A) FT does not support any VM with more than 2 vCPUs regardless of edition
B) FT vCPU count is unlimited as long as hosts are in an EVC cluster
C) FT requires the VM to be reduced to 1 vCPU because vLockstep only supports single-processor VMs
D) FT supports up to 8 vCPUs per protected VM only with Enterprise Plus licensing; Standard edition FT is limited to 2 vCPUs

<details>
<summary>Answer</summary>

**Correct: D**

Symmetric Multiprocessor FT (SMP-FT) supports protected VMs with up to 8 vCPUs, but this capability requires Enterprise Plus licensing; lower editions restrict FT to 2 vCPUs.

**Why the others are wrong:**
- The 2-vCPU limit applies only to lower license editions, not universally — Enterprise Plus supports up to 8 vCPUs.
- There is a hard maximum of 8 vCPUs for FT-protected VMs; it is not unlimited even with EVC enabled.
- vLockstep was the legacy single-vCPU technology; current FT uses Fast Checkpointing, which supports multi-vCPU VMs up to the 8-vCPU limit.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** In a vSphere HA cluster, what role does the elected master host perform that agent hosts do not?

A) It runs all powered-on VMs during normal operation to simplify failover
B) It becomes the vCenter Server for the cluster if vCenter fails
C) It replicates the vCenter Server database locally for redundancy
D) It monitors the health of agent hosts and VMs, and orchestrates VM restarts after a failure

<details>
<summary>Answer</summary>

**Correct: D**

The elected HA master host monitors the state of all agent hosts and protected VMs, tracks cluster membership and resource usage, and coordinates VM restarts when a failure occurs.

**Why the others are wrong:**
- VMs run wherever DRS/HA place them; the master does not host all VMs by default.
- The master host does not replace vCenter Server — HA continues to function even if vCenter is unreachable, but it does not act as a vCenter substitute.
- There is no vCenter database replication performed by the HA master; that is unrelated to HA's function.

</details>

---

**Q8.** An administrator wants to take a snapshot of a VM currently protected by vSphere Fault Tolerance for a backup job. What must be done first?

A) Nothing — FT-protected VMs fully support snapshots natively
B) Migrate the VM to a host without FT enabled using Storage vMotion
C) Convert the VM's virtual disks to physical RDMs before snapshotting
D) Temporarily disable/turn off FT on the VM before taking the snapshot, then re-enable FT afterward

<details>
<summary>Answer</summary>

**Correct: D**

vSphere FT does not support snapshots while FT is active. To take a snapshot (e.g., for backup), FT must be turned off first and can be re-enabled after the snapshot operation completes.

**Why the others are wrong:**
- Snapshots are explicitly unsupported on FT-protected VMs while FT is enabled — this is a core FT limitation tested on the exam.
- Storage vMotion is unrelated to enabling snapshot support and does not resolve the FT/snapshot incompatibility.
- Physical RDMs are actually unsupported with FT and would make the configuration invalid, not fix the snapshot issue.

</details>

---

