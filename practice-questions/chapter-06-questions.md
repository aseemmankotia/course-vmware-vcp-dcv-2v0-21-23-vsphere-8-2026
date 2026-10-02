## Chapter 6: vSAN and Storage Policy-Based Management (SPBM) — Practice Questions

**Q1.** A cluster must run a VM's disk with RAID-6 erasure coding to achieve FTT=2 with minimal capacity overhead. What is the minimum number of vSAN hosts required to support this configuration?

A) 3 hosts
B) 4 hosts
C) 6 hosts
D) 5 hosts

<details>
<summary>Answer</summary>

**Correct: C**

RAID-6 erasure coding uses a 4+2 data/parity scheme, which requires a minimum of 6 hosts (or fault domains) in the cluster.

**Why the others are wrong:**
- 3 hosts only supports RAID-1 FTT=1 (2 data copies + witness).
- 4 hosts is the minimum for RAID-5 (3+1), which only provides FTT=1, not FTT=2.
- 5 hosts is the minimum for RAID-1 mirroring at FTT=2, not RAID-6.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A VM requires tolerance for two simultaneous host failures while minimizing raw storage consumption. Which Storage Policy setting BEST meets this requirement?

A) FTT=2, RAID-1 (Mirroring)
B) FTT=2, RAID-6 (Erasure Coding)
C) FTT=1, RAID-5 (Erasure Coding)
D) FTT=3, RAID-1 (Mirroring)

<details>
<summary>Answer</summary>

**Correct: B**

RAID-6 at FTT=2 tolerates two failures with only 1.5x capacity overhead versus 3x for RAID-1 mirroring at the same FTT level, meeting the requirement with far less raw capacity.

**Why the others are wrong:**
- RAID-1 at FTT=2 also tolerates two failures but consumes 3x the VM's storage (3 full copies), which is not minimal.
- RAID-5 FTT=1 only tolerates a single failure, not two.
- FTT=3 RAID-1 tolerates three failures and requires 7 hosts and 4x capacity — more than required and mirror-only, not erasure coding.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An organization deploys a two-node vSAN cluster for a remote office. Including the witness appliance, how many total components (data hosts + witness) are required at minimum?

A) 2
B) 4
C) 3
D) 5

<details>
<summary>Answer</summary>

**Correct: C**

A two-node vSAN cluster consists of 2 physical ESXi data hosts plus a separate witness host (physical or virtual appliance) located at a third site, totaling 3 components.

**Why the others are wrong:**
- 2 covers only the data hosts and ignores the mandatory witness component.
- 4 is not required — vSAN two-node does not need an additional host beyond the two data nodes and one witness.
- 5 vastly overstates the requirement; two-node topology is specifically designed to minimize hardware to 2 hosts + 1 witness.

</details>

---

**Q4.** A customer wants array-based snapshots, replication, and QoS to be applied at the individual VMDK level, offloading these data services from the ESXi host to the storage array itself. Which vSphere storage architecture should be selected?

A) Virtual Volumes (vVols)
B) Traditional VMFS on a Fibre Channel LUN
C) NFS datastore
D) vSAN OSA with per-VM storage policies

<details>
<summary>Answer</summary>

**Correct: A**

vVols map each VM object (config, data, swap) directly to the array, allowing the array's native snapshot, replication, and QoS engines to operate per-VM instead of per-LUN, using the VASA provider for control-plane awareness.

**Why the others are wrong:**
- Traditional VMFS applies array services at the LUN level, affecting all VMs sharing that datastore, not per-VM.
- NFS datastores similarly apply data services at the volume/export level, not per individual VM object.
- vSAN OSA is a hyperconverged software-defined solution and does not offload data services to an external array — it has no protocol endpoint/VASA array integration model.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** In a vSAN Original Storage Architecture (OSA) hybrid disk group, which device type is used exclusively for the cache tier?

A) SSD (flash)
B) NVMe capacity drive
C) SATA HDD
D) SAS HDD

<details>
<summary>Answer</summary>

**Correct: A**

In OSA, the cache tier device is always an SSD (flash), regardless of whether the disk group is hybrid or all-flash. In hybrid groups it serves as both read cache and write buffer.

**Why the others are wrong:**
- NVMe drives are commonly used as capacity devices in all-flash configurations, not designated cache in hybrid groups by default policy naming.
- SATA HDD is a valid capacity tier device in hybrid disk groups, not a cache device.
- SAS HDD is also a capacity tier device option in hybrid configurations, never used for cache.

</details>

---

**Q6.** What is the primary architectural difference between vSAN Express Storage Architecture (ESA) and Original Storage Architecture (OSA)?

A) ESA requires vCenter while OSA does not
B) ESA only supports RAID-1 mirroring, while OSA supports erasure coding
C) ESA is only available for stretched clusters
D) ESA eliminates the concept of separate disk groups, using a single storage pool per host across all-flash NVMe devices

<details>
<summary>Answer</summary>

**Correct: D**

ESA removes the cache/capacity disk group model entirely, aggregating all claimed high-performance NVMe devices per host into a single storage pool and using a log-structured file system for native erasure coding without a separate caching tier.

**Why the others are wrong:**
- Both ESA and OSA are managed through vCenter; this is not a differentiator.
- ESA actually improves erasure coding efficiency (RAID-5/6 with lower overhead) compared to OSA, so this reverses the fact.
- ESA is a general-purpose architecture applicable to standard, two-node, and stretched clusters, not limited to stretched topology.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** For a vSAN stretched cluster spanning two data sites plus a witness site, which round-trip time (RTT) requirement applies between the two active data sites?

A) ≤5ms
B) ≤1ms
C) ≤50ms
D) ≤200ms

<details>
<summary>Answer</summary>

**Correct: A**

VMware requires a maximum RTT of 5ms between the two active/active data sites in a vSAN stretched cluster to maintain synchronous replication performance.

**Why the others are wrong:**
- 1ms is stricter than the actual documented requirement and is not the published limit.
- 50ms far exceeds the supported RTT for data-site-to-data-site synchronous replication in a stretched cluster.
- 200ms is associated with witness-to-site RTT tolerances in certain configurations, not the data-site-to-data-site requirement.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** By default, how long does vSAN wait before starting a full resync of an object with an absent component (e.g., after a host reboot or transient failure)?

A) 5 minutes
B) 60 minutes
C) 15 minutes
D) 24 hours

<details>
<summary>Answer</summary>

**Correct: B**

The vSAN Object Repair Timer defaults to 60 minutes, giving a transient failure time to recover before vSAN commits to a full resync/rebuild of the affected components.

**Why the others are wrong:**
- 5 minutes is too short and would trigger unnecessary resyncs for brief, recoverable outages.
- 15 minutes is not the default value used by vSAN's Object Repair Timer setting.
- 24 hours would delay protection restoration far longer than the actual conservative default.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

