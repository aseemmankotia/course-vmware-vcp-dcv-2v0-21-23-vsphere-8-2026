## Chapter 8: Snapshots, Clones, and vMotion/Storage vMotion — Practice Questions

**Q1.** A VM has been running with a single snapshot for over 90 days. The datastore is now critically low on free space, and the snapshot's delta disk keeps growing. An administrator attempts to delete the snapshot, but the operation fails with a 'consolidation needed' warning and insufficient space error. What is the BEST immediate action?

A) Power off the VM and manually delete the -delta.vmdk files from the datastore browser
B) Increase the snapshot size limit in vCenter advanced settings
C) Storage vMotion the VM to a datastore with more free space, then retry the snapshot delete/consolidation
D) Convert the VM to a linked clone to reduce the delta disk size

<details>
<summary>Answer</summary>

**Correct: C**

Storage vMotion relocates all VM files including delta disks to a datastore with sufficient free space, which resolves the space constraint so consolidation (merging delta into base disk) can complete without manual file manipulation.

**Why the others are wrong:**
- Manually deleting delta files corrupts the disk chain and can render the VM unbootable — VMware never recommends manual file deletion for active snapshot chains
- There is no such advanced setting; snapshot growth is limited only by datastore free space, not a configurable size limit
- Linked clones are a separate feature (child VMs referencing a parent); converting an existing VM with a live snapshot to a linked clone is not a valid operation to fix consolidation

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A company wants to deploy 50 isolated VDI-style test VMs that must remain fully functional even if the original template is deleted, and each VM needs its own complete, independent virtual disk with no dependency on a parent image. Which VM cloning method should be used?

A) Full clone
B) Linked clone
C) Instant clone
D) Snapshot-based clone

<details>
<summary>Answer</summary>

**Correct: A**

A full clone copies the entire virtual disk into a new, completely independent VM with no reference back to the parent, so deleting the source template has no impact on the clone.

**Why the others are wrong:**
- A linked clone uses delta disks that reference the parent's base disk; deleting or moving the parent breaks the clone
- Instant clones (used for VDI at scale) share a running parent VM's memory and disk state and are not fully independent
- There is no VMware feature called 'snapshot-based clone'; snapshots are a point-in-time state, not a clone type

</details>

---

**Q3.** A cluster contains ESXi hosts with Intel CPUs from three different generations. vMotion between the oldest and newest hosts fails due to CPU incompatibility. Which configuration should the administrator apply to allow vMotion across all hosts in the cluster?

A) Enable Storage vMotion for all VMs in the cluster
B) Configure an EVC baseline matching the newest CPU generation in the cluster
C) Add a second vMotion VMkernel adapter to each host
D) Configure an Enhanced vMotion Compatibility (EVC) baseline matching the oldest CPU generation in the cluster

<details>
<summary>Answer</summary>

**Correct: D**

EVC masks all hosts in the cluster to present the CPU feature set of the lowest common denominator (oldest generation), allowing vMotion compatibility across mixed CPU generations of the same vendor.

**Why the others are wrong:**
- Storage vMotion migrates disk files between datastores; it does not address CPU feature compatibility
- Setting the baseline to the newest generation would expose features the older hosts lack, causing vMotion to still fail on those hosts
- Additional vMotion NICs improve network throughput/multi-NIC vMotion performance but do not resolve CPU instruction set incompatibility

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** An administrator needs to migrate a running VM's virtual disks from an aging SAN datastore to a new all-flash datastore without any downtime, and without changing which ESXi host is running the VM. Which vSphere feature should be used?

A) vMotion
B) vMotion without shared storage
C) Cold migration
D) Storage vMotion

<details>
<summary>Answer</summary>

**Correct: D**

Storage vMotion relocates a running VM's disk files between datastores with zero downtime while the VM stays on the same host, exactly matching the stated requirement.

**Why the others are wrong:**
- Standard vMotion migrates the VM's compute (memory/CPU state) between hosts, not its disk files between datastores
- vMotion without shared storage combines a host migration with a storage migration simultaneously — unnecessary here since the host isn't changing
- Cold migration requires powering off the VM, which violates the zero-downtime requirement

</details>

---

**Q5.** A VM needs to be migrated from a host with only local storage to a different host that also uses only local (non-shared) storage, with the VM remaining powered on throughout. Which migration approach satisfies this requirement?

A) vMotion without shared storage (combined compute and storage migration)
B) Standard vMotion
C) Storage vMotion only
D) Cold migration with a snapshot

<details>
<summary>Answer</summary>

**Correct: A**

vMotion without shared storage copies both the VM's memory state and its disk files across the network in a single live operation, which is exactly what's needed when source and destination hosts don't share a datastore.

**Why the others are wrong:**
- Standard vMotion requires shared storage accessible to both hosts, which doesn't exist in this scenario
- Storage vMotion alone moves disk files but does not migrate the running VM to a different host's compute
- Cold migration requires powering off the VM, violating the requirement that it remain live

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** Which of the following is a required prerequisite specifically for standard (compute-only) vMotion, but NOT a hard requirement for vMotion without shared storage?

A) A vMotion-enabled VMkernel adapter on each host
B) CPU compatibility or an EVC baseline
C) The VM must not have any active snapshots
D) Shared storage accessible by both source and destination hosts

<details>
<summary>Answer</summary>

**Correct: D**

Standard vMotion moves only compute state and requires both hosts to see the same datastore holding the VM's files; vMotion without shared storage removes this requirement by also copying the disk data over the network.

**Why the others are wrong:**
- A vMotion-enabled VMkernel adapter is required for all forms of vMotion, shared storage or not
- CPU compatibility/EVC is required for any live migration between hosts regardless of storage configuration
- VMs with snapshots CAN be vMotioned in modern vSphere versions; this is not a blocking prerequisite for either method

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** What is the maximum supported number of snapshots in a single snapshot chain for one VM in vSphere?

A) 32
B) 10
C) 16
D) Unlimited, limited only by datastore space

<details>
<summary>Answer</summary>

**Correct: A**

VMware supports up to 32 snapshots in a chain per VM, though best practice recommends keeping no more than 2-3 and removing them within 24-72 hours.

**Why the others are wrong:**
- 10 is not the documented VMware maximum for a snapshot chain
- 16 is not the documented VMware maximum for a snapshot chain
- While datastore space affects delta disk growth, the snapshot chain itself has a documented hard limit of 32 regardless of available space

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** When a snapshot is taken with the 'Snapshot the virtual machine's memory' option selected, what additional file is created compared to a snapshot taken without this option?

A) A second -delta.vmdk file for redundancy
B) A .vswp file containing the VM's swap state
C) A .vmsd file recording snapshot metadata
D) A .vmsn file containing the VM's memory state

<details>
<summary>Answer</summary>

**Correct: D**

The .vmsn (snapshot memory) file captures the running memory state at snapshot time, enabling the VM to be reverted to a running, rather than crash-consistent, state.

**Why the others are wrong:**
- Only one delta disk is created per virtual disk regardless of the memory option; memory state is stored separately, not as a second delta
- The .vswp file is the VM's runtime swap file and exists independently of snapshot operations
- The .vmsd file exists for every snapshot (with or without memory) and stores snapshot metadata/hierarchy, not memory contents

</details>

---

