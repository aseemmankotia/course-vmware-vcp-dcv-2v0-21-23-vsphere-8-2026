## Chapter 11: Security, Roles, Lifecycle Management, and Performance Troubleshooting — Practice Questions

**Q1.** A user is granted the 'Virtual Machine Power User' role with propagation enabled on a VM folder. An administrator later assigns that same user the 'Read-Only' role directly on one specific VM inside that folder, with no propagation change. What is the user's effective permission on that VM?

A) Read-Only, because a permission defined directly on an object overrides one inherited from a parent
B) Virtual Machine Power User, because folder-level assignments always take precedence
C) The privileges from both roles are merged into a combined effective permission
D) No Access, because conflicting role assignments are automatically denied

<details>
<summary>Answer</summary>

**Correct: A**

vSphere permission resolution always favors an explicit permission defined directly on the object itself over any permission inherited from a parent, regardless of which role is 'broader'.

**Why the others are wrong:**
- Propagation flows downward, not upward in precedence — folder assignment does not override a closer, direct assignment.
- vSphere does not merge conflicting role privileges from different levels of the hierarchy; the local assignment simply wins.
- There is no automatic deny rule; only an explicit 'No Access' assignment produces that result.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An administrator wants to convert a cluster of ESXi 8 hosts from legacy baseline-based patching to vLCM cluster image management. Which statement about this migration is correct?

A) The cluster can use baselines and a cluster image at the same time, letting admins choose per host
B) Conversion requires a vSAN license because vLCM only functions on vSAN-enabled clusters
C) Firmware and driver updates must still be applied manually outside vLCM even after conversion
D) vLCM automatically validates the desired image against hardware compatibility, and once converted the cluster can no longer use baselines

<details>
<summary>Answer</summary>

**Correct: D**

A cluster is exclusively managed by either baselines or an image — never both — and vLCM performs hardware compatibility validation (including via a Hardware Support Manager) against the desired image.

**Why the others are wrong:**
- Mixing baselines and images in the same cluster is not supported; a cluster is one mode or the other.
- vLCM works on any supported ESXi cluster and does not require vSAN.
- vLCM can manage firmware and driver add-ons as part of the desired image when integrated with a Hardware Support Manager.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** You need to give junior administrators the ability to power VMs on/off and create or delete snapshots, without letting them modify VM hardware or delete the VM itself. What is the recommended approach?

A) Assign the system Administrator role but restrict it to the VM folder only
B) Directly edit the built-in 'Read-Only' system role to add the needed privileges
C) Clone the closest matching sample role and edit the privilege set to match the requirement
D) Assign 'No Access' at the datacenter level and rely on default inherited privileges

<details>
<summary>Answer</summary>

**Correct: C**

Sample roles like Virtual Machine Power User are templates; best practice is to clone them and adjust the privilege set to create a custom role tailored to the exact requirement.

**Why the others are wrong:**
- The Administrator system role cannot be scoped down to remove privileges — it grants full access wherever assigned.
- System roles (Administrator, Read-Only, No Access) cannot be edited at all.
- 'No Access' assigned at any level blocks visibility and does not grant the needed power/snapshot privileges.

</details>

---

**Q4.** In esxtop, a single-vCPU VM shows a sustained %RDY value of 15. What does this indicate and what threshold does the exam associate with CPU contention?

A) CPU scheduling contention — sustained %RDY above roughly 5-10% per vCPU is considered high
B) Normal behavior — %RDY only becomes a concern above 50% per vCPU
C) Memory contention, since %RDY measures memory ballooning, not CPU
D) Storage contention caused by high DAVG values propagating into %RDY

<details>
<summary>Answer</summary>

**Correct: A**

%RDY represents CPU ready time per vCPU; sustained values above roughly 5-10% per vCPU indicate the VM is waiting for physical CPU scheduling and points to overcommitment or scheduling contention.

**Why the others are wrong:**
- 50% is far too high a threshold — contention is flagged well before that point.
- %RDY is a CPU scheduler metric, unrelated to memory ballooning.
- %RDY is unrelated to disk latency counters like DAVG.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A company requires all certificates in vSphere to chain up to their internal enterprise root CA for compliance, but still wants VMCA to automatically issue and renew solution-user and machine certificates without manual intervention. Which configuration should be used?

A) Switch vCenter to Custom certificate mode and manually replace every certificate
B) Enable legacy Thumbprint mode for all ESXi hosts
C) Configure VMCA as a subordinate (intermediate) CA under the enterprise root CA
D) Leave VMCA in default mode and manually import the enterprise root into each ESXi trust store

<details>
<summary>Answer</summary>

**Correct: C**

Replacing VMCA's root certificate with one signed by the enterprise CA lets VMCA continue automatically issuing and renewing certificates while ensuring they chain to the corporate root.

**Why the others are wrong:**
- Custom mode removes VMCA's automatic issuance/renewal entirely, requiring manual management of every certificate.
- Thumbprint mode is a deprecated legacy compatibility mode, not a compliance solution and not recommended for new deployments.
- Leaving VMCA in default self-signed mode does not satisfy the requirement that certificates chain to the enterprise root.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A GSS support engineer needs an ESXi support bundle that includes a live esxtop performance snapshot in addition to standard logs. Which command accomplishes this?

A) vm-support
B) esxcli system support export
C) vm-support -p -d 300 -i 5
D) vim-cmd hostsvc/support/collect

<details>
<summary>Answer</summary>

**Correct: C**

The -p flag captures a live performance snapshot (equivalent to esxtop data), with -d specifying capture duration and -i the sample interval; this is the exact syntax used in escalations.

**Why the others are wrong:**
- Plain vm-support collects configuration files and logs but does not include a live performance snapshot.
- esxcli system support export is not the correct namespace/command for generating a full support bundle.
- This is not valid syntax for triggering a support bundle collection on ESXi.

</details>

---

**Q7.** esxtop's disk view shows KAVG consistently above 2ms while DAVG stays below 1ms on a datastore. What does this indicate?

A) The physical storage array itself is the bottleneck
B) Queuing is occurring inside the VMkernel storage stack, indicating the HBA/LUN queue depth is being exceeded
C) The guest OS storage driver is misconfigured
D) Network latency between the VM and the guest application is high

<details>
<summary>Answer</summary>

**Correct: B**

KAVG reflects time I/O spends queued in the VMkernel before being sent to the device; high KAVG with low DAVG points to queue depth exhaustion inside ESXi, not the physical array.

**Why the others are wrong:**
- A slow physical array would show up as high DAVG, which is low in this scenario.
- GAVG (guest-observed latency), not KAVG, would reflect guest driver issues, and this scenario points to the kernel queue specifically.
- Network latency is not represented by the DAVG/KAVG/GAVG disk latency counters.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** A VM configured with 8 vCPUs shows a high %CSTP value in esxtop while the underlying host has only 8 physical cores available for scheduling. What is the correct remediation?

A) Increase the VM's CPU reservation to guarantee scheduling priority
B) Enable CPU affinity to pin the VM's vCPUs to specific physical cores
C) Add more vRAM to the VM to reduce co-scheduling delays
D) Reduce the number of vCPUs assigned to the VM to better match the actual parallel workload

<details>
<summary>Answer</summary>

**Correct: D**

%CSTP (co-stop) rises when an SMP VM is oversized relative to available physical cores or actual workload parallelism; the fix is reducing vCPU count to match real demand.

**Why the others are wrong:**
- Reservations affect scheduling priority for CPU time but do not resolve co-scheduling delay caused by oversized vCPU count.
- CPU affinity can worsen scheduling flexibility and is not a recommended fix for co-stop.
- Memory allocation is unrelated to CPU co-scheduling and %CSTP.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

