## Chapter 5: Datastores: VMFS, NFS, Storage Adapters, and Multipathing — Practice Questions

**Q1.** A company wants to secure NFS datastore traffic with user-based authentication (not just IP/host-based) between ESXi hosts and the NAS array. Which configuration meets this requirement?

A) NFS 3 datastore with AUTH_SYS authentication
B) NFS 3 datastore with CHAP authentication enabled
C) NFS 4.1 datastore with Kerberos (krb5) authentication
D) NFS 4.1 datastore with AUTH_SYS authentication

<details>
<summary>Answer</summary>

**Correct: C**

NFS 4.1 is the only NFS version ESXi supports with Kerberos (krb5/krb5i), providing user-based authentication instead of host/IP-based trust.

**Why the others are wrong:**
- NFS 3 only supports AUTH_SYS (host-based trust), no Kerberos.
- CHAP is an iSCSI authentication mechanism, not applicable to NFS.
- AUTH_SYS is host-based trust, not user-based, and does not satisfy the requirement even on NFS 4.1.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An administrator wants to minimize ESXi host CPU overhead when connecting to iSCSI storage by offloading iSCSI protocol processing to dedicated hardware. Which adapter type should be selected?

A) Software iSCSI initiator
B) Independent hardware iSCSI adapter
C) Dependent hardware iSCSI adapter
D) NVMe over TCP adapter

<details>
<summary>Answer</summary>

**Correct: B**

Independent hardware iSCSI adapters fully offload iSCSI configuration, initiator functions, and network processing (TCP/IP and iSCSI stack) from the ESXi CPU.

**Why the others are wrong:**
- Software iSCSI uses the VMkernel network stack and ESXi CPU for all iSCSI processing — highest CPU usage.
- Dependent hardware iSCSI still relies on ESXi's networking configuration and stack; only partial offload occurs.
- NVMe over TCP is a separate transport for NVMe, not iSCSI, and still uses host CPU for TCP processing.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A cluster running Microsoft Failover Clustering (WSFC) with nodes on separate ESXi hosts requires shared disk access using SCSI-3 persistent reservations passed directly to the guest OS. Which RDM mode must be used?

A) Physical compatibility mode RDM
B) Virtual compatibility mode RDM
C) VMFS6 thin-provisioned virtual disk
D) NFS 4.1 datastore with independent-persistent disk

<details>
<summary>Answer</summary>

**Correct: A**

Physical compatibility mode RDM passes almost all SCSI commands directly to the underlying LUN, including SCSI-3 reservations required for cross-host WSFC configurations.

**Why the others are wrong:**
- Virtual mode RDM virtualizes the LUN's SCSI attributes and does not support the SCSI-3 reservation pass-through needed for cross-host clustering.
- A regular VMDK on VMFS doesn't provide the raw LUN access WSFC requires.
- NFS datastores don't support raw device mapping to a physical LUN.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** You are adding an iSCSI target and already know its exact IQN and IP address, and you don't want ESXi to query the array for all available targets. Which discovery method should you configure?

A) Dynamic (SendTargets) discovery
B) iSNS discovery
C) CHAP discovery
D) Static discovery

<details>
<summary>Answer</summary>

**Correct: D**

Static discovery lets you manually enter the target IQN and IP without querying the array, which is exactly the scenario described.

**Why the others are wrong:**
- Dynamic (SendTargets) discovery queries the array and returns all available targets automatically — not what's requested.
- iSNS is a naming service for locating targets on the network, not a manual entry method.
- CHAP is an authentication protocol, not a discovery method.

</details>

---

**Q5.** Which statement correctly differentiates the Fixed and Most Recently Used (MRU) Path Selection Policies in NMP?

A) Fixed distributes I/O across all active paths; MRU always uses only one designated preferred path
B) MRU reverts to the preferred path automatically; Fixed does not support a preferred path
C) Fixed and MRU are functionally identical except for their default PSP assignment
D) Fixed reverts to the preferred path when it becomes available again; MRU continues using the current active path even after the preferred path returns

<details>
<summary>Answer</summary>

**Correct: D**

Fixed uses a designated preferred path and fails back to it once restored. MRU has no concept of a preferred path — it keeps using whichever path was most recently active, even after the original path is restored.

**Why the others are wrong:**
- Distributing I/O across all active paths describes Round Robin, not Fixed.
- This reverses the actual behavior — MRU does not have a preferred path concept at all.
- They differ significantly in failback behavior, which is a key exam distinction.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** An administrator configures Round Robin PSP on a datastore. By default, after how many I/O operations sent down a single path does NMP switch to the next active path?

A) 10 I/Os
B) 100 I/Os
C) 10000 I/Os
D) 1000 I/Os

<details>
<summary>Answer</summary>

**Correct: D**

The Round Robin PSP default IOPS limit is 1000 I/O operations per path (or 10 MB of data) before switching to the next active path.

**Why the others are wrong:**
- 10 is far too low and not the documented default.
- 100 is not the VMware default value.
- 10000 is not the default; this would drastically underutilize multipathing.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** What is the correct relationship between the Storage Array Type Plugin (SATP) and Path Selection Policy (PSP) within the Native Multipathing Plugin (NMP) architecture?

A) SATP handles array-specific operations like failover; PSP determines the path used to send I/O
B) SATP selects which path to use for I/O; PSP handles array-specific failover events
C) SATP and PSP are two names for the same component
D) PSP is only used for Fibre Channel arrays, while SATP is used for iSCSI and NVMe-oF arrays

<details>
<summary>Answer</summary>

**Correct: A**

SATP handles array-specific tasks such as detecting path failures and performing failover; PSP determines which physical path is used to send I/O requests for a given device.

**Why the others are wrong:**
- This reverses their roles entirely.
- They are distinct plugins with different responsibilities within NMP.
- Both SATP and PSP apply regardless of the underlying protocol (FC, iSCSI, NVMe-oF).

</details>

---

**Q8.** A storage team wants to enable one-way CHAP so the ESXi initiator authenticates to the iSCSI target, but the target does NOT authenticate back to the initiator. Which CHAP configuration should be used?

A) Mutual CHAP
B) Bidirectional CHAP
C) Unidirectional (one-way) CHAP
D) Kerberos-based CHAP

<details>
<summary>Answer</summary>

**Correct: C**

Unidirectional (one-way) CHAP authenticates only the initiator to the target; the target does not need to authenticate itself back to the initiator.

**Why the others are wrong:**
- Mutual CHAP requires both sides to authenticate each other — this is two-way, not one-way.
- Bidirectional CHAP is another name for mutual CHAP, contradicting the requirement.
- Kerberos-based CHAP is not a real CHAP variant; Kerberos is used with NFS 4.1, not iSCSI CHAP.

</details>

---

