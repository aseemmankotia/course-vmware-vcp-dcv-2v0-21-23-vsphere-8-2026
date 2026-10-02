## Chapter 2: vCenter Server Deployment and Inventory Design — Practice Questions

**Q1.** A customer is planning to manage 550 ESXi hosts and 6,000 VMs from a single vCenter Server Appliance. Which deployment size meets this requirement with the least oversized footprint?

A) Small
B) Medium
C) Large
D) X-Large

<details>
<summary>Answer</summary>

**Correct: C**

Large supports up to 1,000 hosts and 10,000 VMs, comfortably covering 550 hosts/6,000 VMs without the extra overhead of X-Large.

**Why the others are wrong:**
- Small only supports up to 100 hosts and 1,000 VMs — far below the requirement.
- Medium supports up to 400 hosts and 4,000 VMs — the host count of 550 exceeds this limit.
- X-Large supports up to 2,000 hosts and 35,000 VMs — technically works but is oversized and wastes resources versus Large.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An administrator wants to manage three vCenter Server instances from a single vSphere Client session without deploying an external Platform Services Controller. What must be true for this to work in current vSphere releases?

A) Each vCenter Server must deploy its own external PSC and register it with a load balancer
B) Enhanced Linked Mode requires vCenter Server instances to be in different SSO domains
C) Enhanced Linked Mode is only available in the vCenter Server Standard edition, not Foundation
D) All three vCenter Server instances must join the same SSO domain to enable Enhanced Linked Mode

<details>
<summary>Answer</summary>

**Correct: D**

Since vSphere 7.0, the embedded architecture supports Enhanced Linked Mode natively as long as all vCenter Server instances share the same SSO domain — no external PSC is needed.

**Why the others are wrong:**
- External PSC deployment was deprecated/removed starting in vSphere 7.0; it is not required or supported for new ELM setups.
- ELM specifically requires the SAME SSO domain, not different domains.
- Edition licensing does not control whether ELM is available; SSO domain membership does.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A company runs a single vCenter Server Appliance that is critical to daily operations. They need to minimize downtime if the appliance VM or its host fails, without relying on external backup software. Which built-in feature should they configure?

A) vCenter Server file-based backup via VAMI
B) vSphere HA on the management cluster only
C) Enhanced Linked Mode with a second vCenter instance
D) vCenter High Availability (vCenter HA)

<details>
<summary>Answer</summary>

**Correct: D**

vCenter HA creates an Active-Passive-Witness cluster of appliance nodes, automatically failing over the vCenter Server role if the active node or its host fails.

**Why the others are wrong:**
- File-based backup protects configuration data for restore after a failure but does not provide automatic failover or minimize downtime.
- vSphere HA protects VMs running on the cluster (including the vCenter Server VM) by restarting them, but it does not provide the near-continuous availability or state synchronization vCenter HA offers.
- Enhanced Linked Mode links multiple independent vCenter Server instances for unified inventory viewing; it does not provide automatic failover of a single instance.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Which vCenter inventory object is used exclusively to allocate and control CPU and memory resources for a group of VMs, without providing storage or network organization?

A) Folder
B) Resource Pool
C) Cluster
D) Datacenter

<details>
<summary>Answer</summary>

**Correct: B**

Resource pools partition CPU and memory (shares, reservations, limits) among VMs or nested pools; they do not manage storage or networking.

**Why the others are wrong:**
- Folders organize objects (VMs, hosts, datastores, networks) for permissions and organization, but do not control resource allocation.
- A cluster aggregates host compute/storage resources and enables features like DRS/HA; it is a container above resource pools, not a resource-control object itself.
- A datacenter is the top-level container for hosts, clusters, VMs, datastores, and networks; it has no resource allocation function.

</details>

---

**Q5.** During vCenter Server Appliance deployment, at which stage are the appliance size (Tiny/Small/Medium/Large/X-Large) and target ESXi host or vCenter selected?

A) Stage 2 – Appliance configuration
B) Stage 1 – OVA deployment
C) Post-deployment SSO configuration
D) vCenter HA cluster configuration wizard

<details>
<summary>Answer</summary>

**Correct: B**

Stage 1 of the VCSA installer handles OVA deployment: target host selection, appliance name, deployment size, storage size, and network settings.

**Why the others are wrong:**
- Stage 2 configures the already-deployed appliance: NTP, SSO domain, and other post-deployment settings — sizing is already fixed by this point.
- SSO domain configuration is part of Stage 2, not related to sizing selection.
- vCenter HA configuration happens after the appliance is fully deployed and operational; it does not involve initial sizing.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A company needs to authenticate vCenter Server users against their existing Active Directory without deploying a standalone identity server. What should the administrator configure in vCenter Single Sign-On?

A) Configure Enhanced Linked Mode to sync AD users automatically
B) Deploy a new external Platform Services Controller for AD integration
C) Enable vCenter HA and assign AD credentials to the witness node
D) Add Active Directory over LDAPS as an identity source in SSO

<details>
<summary>Answer</summary>

**Correct: D**

vCenter SSO supports adding Active Directory (over LDAPS) as an identity source directly, allowing AD users/groups to authenticate without extra infrastructure.

**Why the others are wrong:**
- Enhanced Linked Mode links multiple vCenter Server SSO domains for inventory visibility; it has nothing to do with identity source configuration.
- External PSC deployment is deprecated and unnecessary — SSO identity sources are configured directly on the embedded vCenter.
- vCenter HA is a resiliency feature for the appliance itself, unrelated to identity source or authentication configuration.

</details>

---

**Q7.** An administrator schedules a recurring file-based backup of the vCenter Server Appliance to a network share. What does this backup type primarily protect?

A) Full appliance VM disk image including the guest OS
B) vCenter Server configuration, inventory, and core database contents
C) ESXi host configuration files across the entire cluster
D) vSAN datastore metadata and object placement policies

<details>
<summary>Answer</summary>

**Correct: B**

File-based backup captures the vCenter Server configuration, inventory, and embedded database (PostgreSQL) contents so the appliance can be restored via the installer's Restore workflow.

**Why the others are wrong:**
- A full disk image backup is an image-based (VM-level) backup, not the native file-based backup mechanism.
- ESXi host configuration is managed separately (e.g., via Host Profiles) and is not the target of a vCenter file-based backup.
- vSAN metadata is stored and protected within vSAN itself, not by the vCenter Server file-based backup process.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which statement about the Platform Services Controller (PSC) is accurate for current vSphere versions?

A) External PSC is required for deployments with more than 5 vCenter Server instances
B) PSC functionality is now embedded directly into the vCenter Server Appliance and external PSC is no longer supported for new deployments
C) PSC must be deployed separately to enable Enhanced Linked Mode
D) PSC only exists as a Windows-installable component, never as part of the appliance

<details>
<summary>Answer</summary>

**Correct: B**

Since vSphere 7.0, VMware consolidated PSC services into the embedded vCenter Server Appliance; external PSC deployments are no longer supported for new installs.

**Why the others are wrong:**
- There is no host-count threshold requiring an external PSC — it doesn't exist as a supported option anymore.
- Enhanced Linked Mode now works via embedded architecture and shared SSO domain membership, not external PSC.
- PSC as a standalone Windows-installable component was part of the legacy vCenter for Windows model, which has been fully deprecated.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

