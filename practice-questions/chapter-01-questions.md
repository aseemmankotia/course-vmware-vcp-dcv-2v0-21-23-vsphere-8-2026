## Chapter 1: vSphere 8 Architecture and ESXi Installation — Practice Questions

**Q1.** An administrator must deploy 100 new ESXi 8 hosts with zero local storage requirements, pulling the image fresh from the network at every single boot so image updates are instantly centralized. Which deployment method meets this requirement?

A) Scripted installation with a kickstart file targeting local disk
B) Auto Deploy in Stateless mode
C) Interactive ISO installation via remote virtual media
D) Auto Deploy in Stateless Caching mode

<details>
<summary>Answer</summary>

**Correct: B**

Stateless Auto Deploy pulls the image profile from the Auto Deploy server over the network on every boot and never persists the image to local storage, satisfying the 'zero local storage' requirement.

**Why the others are wrong:**
- Scripted (kickstart) installs write a permanent image to local disk, contradicting the zero-storage requirement
- Interactive ISO installation requires manual input at each host and installs locally, which does not scale to 100 hosts nor stay network-only
- Stateless Caching writes the image to local disk as a fallback cache, which violates 'zero local storage'

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A host configured with Auto Deploy loses network connectivity to the Auto Deploy server during a maintenance window, but it still boots successfully using the last-known image profile. Which Auto Deploy mode was configured on this host?

A) Stateless
B) Stateful Install
C) Scripted install with a saved answer file
D) Stateless Caching

<details>
<summary>Answer</summary>

**Correct: D**

Stateless Caching stores a copy of the image profile on the host's local disk, allowing the host to boot from that cache if the Auto Deploy server is unreachable.

**Why the others are wrong:**
- Pure Stateless mode requires the Auto Deploy server to be reachable at every boot with no fallback cache
- Stateful Install performs a one-time full install and behaves like a normal ESXi host afterward — it is not the mechanism being described for a caching fallback
- Scripted install is not part of Auto Deploy at all; it is a separate PXE/kickstart-based installation method

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** You are installing ESXi 8.0 on a host that has only a single 16 GB internal USB device and no other local storage. What is the expected outcome?

A) Installation completes normally with both the boot bank and ESX-OSData partition on the USB device
B) The installer fails or warns because ESX-OSData requires a separate persistent storage device of at least 32 GB
C) ESXi automatically relocates ESX-OSData to a datastore on vCenter Server
D) Installation succeeds but permanently disables the scratch partition with no supported workaround

<details>
<summary>Answer</summary>

**Correct: B**

Since ESXi 7.0 U3 (carried into ESXi 8), USB/SD media can only host the boot bank; the ESX-OSData partition (holding /scratch, VMFS-L locker, core dumps) requires a separate persistent device of at least 32 GB, with 128 GB+ SSD/NVMe recommended.

**Why the others are wrong:**
- USB/SD alone can no longer host the full OSData partition due to flash wear and size limitations
- vCenter Server is not involved in host installation; it does not exist yet when ESXi is being installed and cannot host local partitions
- The scratch/OSData location can be reconfigured post-install by pointing it to a persistent device; it is not permanently disabled

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** An administrator needs to set the root password and configure NTP on a freshly installed standalone ESXi 8 host that has not yet been added to vCenter Server. Which tool should be used?

A) vSphere Client connected to vCenter Server
B) ESXi Host Client
C) PowerCLI connected to vCenter Server
D) vSphere Lifecycle Manager

<details>
<summary>Answer</summary>

**Correct: B**

The embedded ESXi Host Client (https://<host-ip>/ui) manages a single standalone host directly and provides full configuration access, including root password and NTP, without requiring vCenter Server.

**Why the others are wrong:**
- vSphere Client requires the host to be added to a vCenter Server inventory, which has not happened yet
- PowerCLI connected to vCenter has the same dependency — vCenter must exist and the host must be registered
- vSphere Lifecycle Manager manages image compliance and updates, not per-host root password or NTP configuration

</details>

---

**Q5.** Before purchasing new server hardware to run ESXi 8, which VMware resource should be checked to confirm the CPU, NIC, and storage controller are supported?

A) VMware Configuration Maximums tool
B) VMware Product Interoperability Matrix
C) VMware Compatibility Guide (VCG)
D) vSphere Lifecycle Manager depot

<details>
<summary>Answer</summary>

**Correct: C**

The VMware Compatibility Guide (vmware.com/compatibility) is the authoritative source for verifying server models, CPUs, storage controllers, and NICs are certified for a specific ESXi version.

**Why the others are wrong:**
- Configuration Maximums lists supported limits (max VMs, max hosts per cluster, etc.), not hardware compatibility
- The Product Interoperability Matrix confirms compatibility between VMware software products/versions, not physical hardware
- The vLCM depot stores update/patch binaries and image components, not hardware certification data

</details>

---

**Q6.** An administrator wants to fully automate the ESXi 8 installation, including network configuration, root password, and license key assignment, with zero interactive prompts. Which method and artifact are required?

A) Interactive installation using a saved answer file
B) Scripted installation using a kickstart (ks.cfg) file
C) Auto Deploy using only a host profile
D) vSphere Lifecycle Manager image-based remediation

<details>
<summary>Answer</summary>

**Correct: B**

Scripted installation uses a kickstart file (ks.cfg) referenced at boot (e.g., ks=usb, ks=nfs://) to fully automate network config, root password, and license key entry without any prompts.

**Why the others are wrong:**
- Interactive installation by definition requires manual prompts; there is no 'saved answer file' mechanism in ESXi interactive installs
- A host profile alone configures settings after deployment and does not drive the initial unattended install itself — it is normally paired with Auto Deploy image profiles, not used alone
- vLCM manages ongoing patching/upgrades of already-installed hosts, not the initial unattended install

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** What is the primary difference between ESXi evaluation mode and an assigned license key?

A) Evaluation mode disables vMotion but keeps all other features enabled
B) Evaluation mode is capped at 8 CPU cores per host
C) Evaluation mode provides full feature access for 60 days; after expiration, new VMs cannot be powered on until a valid license is assigned
D) Evaluation mode requires vCenter Server to be licensed separately from ESXi

<details>
<summary>Answer</summary>

**Correct: C**

ESXi evaluation mode grants full enterprise-level feature access for 60 days from first boot. Running VMs are not powered off at expiration, but no new VM can be powered on until a valid license key is assigned.

**Why the others are wrong:**
- vMotion and all other features remain fully functional during the 60-day evaluation; nothing is disabled
- There is no core-count restriction on evaluation mode itself; core limits relate to per-CPU license capacity, not evaluation
- Evaluation mode and licensing apply per-product; vCenter and ESXi each have separate evaluation periods, but this is not the 'primary difference' being tested here

</details>

---

**Q8.** A vSphere cluster is experiencing intermittent HA reference errors, certificate validation failures, and vMotion failures. Investigation shows ESXi host clocks differ by several minutes across the cluster. Which practice would have prevented this?

A) Increasing the vMotion network MTU to 9000
B) Enabling EVC mode on the cluster
C) Configuring NTP or PTP time synchronization consistently on all hosts and vCenter Server
D) Configuring Auto Deploy Stateless Caching on all hosts

<details>
<summary>Answer</summary>

**Correct: C**

Consistent time synchronization (NTP or PTP) across all ESXi hosts and vCenter Server is required for certificate validity, HA heartbeat/reference checks, and vMotion compatibility checks; clock drift causes exactly these symptoms.

**Why the others are wrong:**
- MTU size affects network throughput/fragmentation, not clock drift or certificate validation
- EVC (Enhanced vMotion Compatibility) masks CPU feature differences for vMotion compatibility, unrelated to time sync issues
- Auto Deploy caching mode relates to image/boot resiliency, not clock synchronization

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

