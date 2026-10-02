# Practice Test 2: VCP-DCV 2V0-21.23: vSphere 8 Exam-Focused Prep

- **Questions:** 54
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-2.md`. Track results in `score-tracker.md`.

---

**Q1.** A company deploys vCenter Server High Availability (VCHA) for its production vCenter Server Appliance using the automatic configuration wizard. Which statement correctly describes the role of the Witness node in this architecture?

A) The Witness node holds a full replicated copy of the vPostgres database and can be manually promoted to Active if both the Active and Passive nodes fail.
B) The Witness node is a lightweight VM that provides quorum only and does not replicate vCenter Server data.
C) The Witness node must be deployed on a completely separate vCenter Server instance for security isolation from the cluster it protects.
D) The Witness node actively services vSphere Client read-only sessions while the Active node is performing failover.

---

**Q2.** An administrator wants to use vSphere Quick Boot to speed up host remediation during a vSphere Lifecycle Manager (vLCM) remediation task on an ESXi 8.0 host that has a TPM 2.0 chip installed and Secure Boot enabled. What happens regarding Quick Boot on this host?

A) Quick Boot is disabled only if the TPM firmware version reports as 1.2 or lower.
B) Quick Boot is automatically disabled on hosts with a TPM 2.0 chip installed, because the reboot must reinitialize the hardware trust chain measured by the TPM.
C) Quick Boot always conflicts with UEFI Secure Boot and cannot be combined under any circumstances, regardless of TPM presence.
D) Quick Boot support requires disabling the TPM temporarily in BIOS, but only during the initial ESXi installation.

---

**Q3.** An administrator is deploying a new vCenter Server Appliance to manage an environment that will grow to 2,000 ESXi hosts and 25,000 powered-on virtual machines. During the stage 1 deployment wizard, which deployment size should be selected to meet this capacity?

A) X-Large (up to 2,000 hosts / 35,000 VMs)
B) Large (up to 1,000 hosts / 10,000 VMs)
C) Medium (up to 400 hosts / 4,000 VMs)
D) Small (up to 100 hosts / 1,000 VMs)

---

**Q4.** Two existing vCenter Server 8.0 Appliances were originally deployed with separate vCenter Single Sign-On domains. The administrator now wants to join them using Enhanced Linked Mode so both appear in a single inventory view. Which approach correctly achieves this without a full redeployment of either appliance?

A) Use the cmsso-util move command on one vCenter Server Appliance to join it into the SSO domain of the other, since both vCenter Servers must belong to the same SSO domain for Enhanced Linked Mode.
B) Nothing extra is needed; Enhanced Linked Mode automatically links vCenter Servers across different SSO domains once both are registered in the same vSphere Client session.
C) Deploy a standalone Platform Services Controller node and point both vCenter Servers at it to bridge the two domains.
D) Enable Enhanced Linked Mode from the vSphere Client by adding one vCenter Server as a managed host inside the other vCenter's inventory.

---

**Q5.** An ESXi 8.0 host has UEFI Secure Boot enabled and also contains a TPM 2.0 chip. What capability does this combination specifically enable that is visible from vCenter Server?

A) It automatically enables encryption for vTPM-enabled virtual machines without requiring a Key Provider configured in vCenter.
B) It enables Encrypted vMotion for all VMs on that host by default, even if Encrypted vMotion is set to 'Disabled' at the VM level.
C) vCenter Server can report the host's boot attestation status (Secure Boot verification) as Passed or Failed on the host's Monitor tab.
D) It allows the host to bypass the requirement for a Key Provider when creating VM Encryption Policies for that host's local datastore.

---

**Q6.** An administrator is performing a fully unattended, scripted installation of ESXi 8.0 via PXE boot, and needs the installer to retrieve its kickstart configuration file from an HTTP server at 192.168.1.10. Which boot option correctly instructs the ESXi installer to load the kickstart file from that location?

A) ksdevice=http://192.168.1.10/ks.cfg
B) install=http://192.168.1.10/ks.cfg
C) ks=http://192.168.1.10/ks.cfg
D) autoinstall=http://192.168.1.10/ks.cfg

---

**Q7.** An administrator is preparing to install ESXi 8.0 on new hosts that will also participate in a vSAN cluster. To meet VMware's best practices for the ESX-OSData partition and avoid redirecting scratch and core dump data to a shared datastore, which boot device configuration should be used?

A) A USB flash drive or SD card of at least 16GB, since vSphere 8 reduced partition size requirements
B) A local persistent storage device, such as an HDD or SSD, of at least 32GB (128GB recommended for vSAN)
C) A remote NFS or iSCSI datastore configured as the boot LUN
D) Any USB 2.0 device of 8GB or greater, as required in previous vSphere versions

---

**Q8.** An administrator is enabling vCenter Server High Availability (vCenter HA) on a vCenter Server Appliance running vSphere 8. Besides adding a second vNIC to each node for HA traffic, what additional network requirement must be satisfied?

A) The HA network can share the same VLAN/subnet as the management network as long as a static route is configured
B) The HA network must be a Layer 3 routed network with a maximum round-trip latency of 100ms
C) The HA network must be configured as a distributed port group tagged with the management VLAN ID to allow failover
D) The HA network must use a separate subnet/VLAN from the management network, with round-trip latency under 10ms between nodes

---

**Q9.** Which statement correctly describes Enhanced Linked Mode (ELM) in vSphere 8?

A) ELM requires vCenter Server Foundation edition and supports linking up to 4 instances
B) ELM links multiple vCenter Server instances (up to 15) that share a common SSO domain, enabling a unified inventory view and search across all linked instances
C) ELM requires an external Platform Services Controller (PSC), an architecture removed since vSphere 7
D) ELM automatically synchronizes DRS and HA cluster configuration settings across all linked vCenter Server instances

---

**Q10.** A vSphere 8 cluster uses Network I/O Control version 3 on a distributed switch shared by vMotion, management, and virtual machine traffic. During peak load, vMotion migrations are timing out because VM traffic consumes all available bandwidth on the 10GbE uplinks. The administrator must guarantee that vMotion always receives at least 2 Gbps, even during congestion, without capping the maximum bandwidth any traffic type can burst to. Which NIOC configuration should be applied to the vMotion system traffic type?

A) Set a Reservation of 2000 Mbps on the vMotion traffic type
B) Set a Limit of 2000 Mbps on the vMotion traffic type
C) Increase the Shares value for vMotion to 100 (High)
D) Move vMotion traffic to a separate standard switch with no NIOC

---

**Q11.** vCenter Server for a customer environment is unreachable due to a database corruption issue, but the operations team must urgently connect a temporary troubleshooting VM to an existing distributed port group directly from the ESXi host's local UI while vCenter is being rebuilt. Which port binding type must have been configured on that distributed port group in advance to allow this?

A) Static binding
B) Dynamic binding
C) Ephemeral binding
D) Fixed binding

---

**Q12.** An administrator is migrating uplinks from a manually configured EtherChannel (static) NIC team using the 'Route based on IP hash' teaming policy to a proper LACP Link Aggregation Group (LAG) on a distributed switch, backed by physical switches configured for dynamic LACP. After creating the LAG and moving the physical NICs into it, which additional step is required on the port group's teaming and failover policy for LACP to function correctly?

A) Manually set 'Route based on IP hash' as the active teaming algorithm for the port group
B) Set the LAG as the only entry in the Active Uplinks list and remove other uplinks from Active/Standby lists
C) Configure NIOC shares of 100 on all traffic types using that LAG
D) Enable promiscuous mode on the port group to allow LACP control frames

---

**Q13.** A security team requires that VMs on a tenant's secondary VLAN segment be able to communicate with each other directly (peer-to-peer) and also reach the default gateway on the primary VLAN, but must NOT be able to communicate with VMs on a different secondary VLAN segment within the same private VLAN structure. Which private VLAN (PVLAN) secondary type should be assigned to this port group?

A) Promiscuous
B) Community
C) Isolated
D) Primary

---

**Q14.** After enabling jumbo frames (MTU 9000) end-to-end for a new IP storage VMkernel adapter, administrators intermittently see storage performance degrade and vMotion operations occasionally fail with fragmentation-related errors, but only for traffic traversing one specific physical uplink. Which built-in vSphere Distributed Switch feature should be enabled first to automatically identify the root cause without manually checking every switch port?

A) NetFlow traffic analysis
B) Distributed switch Health Check (VLAN, MTU, and teaming/failover checks)
C) Port mirroring (SPAN) session
D) Network I/O Control version 3 traffic filtering

---

**Q15.** An administrator is configuring multi-NIC vMotion across two 10GbE physical uplinks (vmnic2 and vmnic3) to load-balance and accelerate a large vMotion migration. Two VMkernel adapters (vmk1 and vmk2) are created on the same distributed port group family for vMotion. Which configuration correctly enables true multi-NIC vMotion load balancing across both uplinks?

A) Place both vmk1 and vmk2 on a single port group with both uplinks marked Active, using default load balancing
B) Create one VMkernel adapter and bind it to both uplinks simultaneously using NIC teaming failback disabled
C) Create two separate port groups, each with an override failover order making one uplink Active and the other Unused, then assign vmk1 to one port group and vmk2 to the other
D) Assign vmk1 and vmk2 to the same port group with both uplinks set to Standby to force alternation

---

**Q16.** A vDS aggregates two 10 GbE uplinks per host, providing 20 Gbps of total capacity, and Network I/O Control version 3 is enabled. The administrator has already reserved the following for system traffic: Management 1 Gbps, vMotion 4 Gbps, vSAN 6 Gbps (11 Gbps total reserved). The administrator now attempts to reserve an additional 5 Gbps for the vSphere Replication traffic type. What happens?

A) The reservation succeeds, but vSAN traffic is automatically throttled to make room for the new reservation.
B) The reservation succeeds because NIOC allows up to 100% of aggregate bandwidth to be reserved among system traffic types.
C) The reservation fails because vSphere Replication does not support bandwidth reservations in NIOC v3.
D) The reservation fails because the total reserved bandwidth for system traffic (16 Gbps) exceeds the default 75% admission control quota (15 Gbps) of the 20 Gbps aggregate capacity.

---

**Q17.** An administrator creates a LACP Link Aggregation Group named lag1 on a distributed switch using two physical uplinks and sets the LAG's own load balancing mode to 'Source and destination IP address and TCP/UDP port.' After creation, VM traffic on the associated port groups is still traversing the original standalone uplinks instead of lag1. What must be changed to make the port groups actually use the LAG?

A) On each port group's teaming and failover policy, move lag1 into the Active Uplinks list and move the standalone uplinks to Unused Uplinks.
B) Recreate the LAG using Enhanced LACP mode instead of Standard mode so port groups automatically switch to it.
C) Enable Network I/O Control on the LAG object so traffic is redirected to it automatically.
D) Set the port group teaming and failover policy to 'Route based on IP hash' and add lag1 as an additional active uplink alongside the standalone uplinks.

---

**Q18.** An administrator configures multi-NIC vMotion on a host with two VMkernel adapters, vmk1 and vmk2, both bound to the same vMotion TCP/IP stack and the same subnet, and both placed on a single distributed port group using 'Route based on originating virtual port' with both uplinks active. During migration of a single large VM, monitoring shows only one physical uplink is utilized while the second sits idle. What is the MOST likely cause?

A) MTU 9000 (jumbo frames) was not enabled on vmk2, causing it to fall into a standby state.
B) The vMotion traffic type's NIOC shares are configured too low on the uplink associated with vmk2.
C) vmk1 and vmk2 were placed in different vMotion TCP/IP stacks, causing vmk2 traffic to be silently dropped.
D) vmk1 and vmk2 should have been placed on two separate port groups, each with an explicit failover order override pinning it to one distinct active uplink and marking the other uplink unused.

---

**Q19.** A vSphere 8 administrator wants automatic space reclamation (UNMAP) on a VMFS-6 datastore to reclaim deleted blocks as fast as possible, accepting the additional host I/O overhead this causes. Which reclamation priority setting, available starting in vSphere 8, should be configured?

A) Low
B) None
C) High
D) Medium

---

**Q20.** A company presents an ALUA-compliant active/passive storage array to an ESXi 8 cluster over Fibre Channel. Which Native Multipathing Plug-in Path Selection Policy is recommended by VMware to balance I/O across the active controller's paths while avoiding path thrashing?

A) Round Robin (RR)
B) Fixed
C) Most Recently Used (MRU)
D) Fixed with a manually set preferred path

---

**Q21.** A vSAN storage policy is configured with 'Failures to Tolerate' set to 2 using RAID-6 (Erasure Coding) for space efficiency. What is the minimum number of hosts contributing storage that the vSAN cluster must have to satisfy this policy?

A) 6
B) 4
C) 5
D) 8

---

**Q22.** A VM is deployed using a storage policy with a tag-based placement rule requiring the datastore to have the tag 'Gold'. After deployment, the administrator removes the 'Gold' tag from the datastore hosting the VM's disks. What happens to the VM as a result?

A) vSphere automatically Storage vMotions the VM to a compliant datastore
B) The VM is powered off until a compliant datastore is available
C) The VM's storage policy compliance status changes to noncompliant, but the VM remains on the same datastore until manually remediated
D) SPBM deletes the VM's virtual disks to enforce policy compliance

---

**Q23.** In a Virtual Volumes (vVols) architecture, which component acts as the data access point between ESXi hosts and the storage array, eliminating the need to present traditional LUNs for per-VM I/O?

A) Protocol Endpoint (PE)
B) VASA Provider
C) Storage Container
D) Config-VVol

---

**Q24.** An administrator wants to increase throughput to a single NFS 4.1 datastore by allowing ESXi to establish multiple TCP connections to the NFS server for the same mount. Which NFS 4.1 feature, requiring support on both ESXi and the NFS server, enables this behavior?

A) Session trunking (multipathing)
B) LACP link aggregation
C) Kerberos with AES encryption
D) Storage I/O Control

---

**Q25.** A vSAN-enabled cluster uses an all-flash configuration with an active/active iSCSI array presenting additional VMFS datastores for legacy VMs still using Round Robin (VMW_PSP_RR) multipathing. An administrator wants to reduce the default IOPS limit from 1000 to 1 on a specific device so I/O is switched to the next path after every single I/O, improving path utilization. Which command accomplishes this on the ESXi host?

A) esxcli storage nmp satp set --satp VMW_SATP_DEFAULT_AA --device naa.60000000000000000000000000000001 --iops 1
B) esxcli storage core device set --device naa.60000000000000000000000000000001 --queue-full-threshold 1
C) esxcli storage nmp psp roundrobin deviceconfig set --device naa.60000000000000000000000000000001 --iops 1 --type iops
D) esxcli storage nmp psp roundrobin deviceconfig set --device naa.60000000000000000000000000000001 --bytes 1 --type bytes

---

**Q26.** An architect is designing a vSAN cluster and must apply a storage policy with Failures to Tolerate (FTT) = 2 using the RAID-1 (Mirroring) fault tolerance method for a critical database VM. Assuming the cluster is a standard (non-stretched) topology, what is the minimum number of hosts contributing storage required in the cluster, and how many full data mirror copies will vSAN create for the object?

A) 3 hosts minimum, 3 full data copies
B) 6 hosts minimum, 3 full data copies
C) 5 hosts minimum, 3 full data copies
D) 5 hosts minimum, 2 full data copies

---

**Q27.** In a vSphere Virtual Volumes (vVols) architecture, which component acts as the actual data-path access point between ESXi hosts and the vVols storage container, receiving all SCSI or NFS I/O for individual virtual volumes?

A) Protocol Endpoint
B) VASA Provider
C) Storage Container
D) Config-VVol

---

**Q28.** An administrator manages a master VM template in a Content Library and wants to make configuration changes while preserving the ability to roll back to the prior version if the update introduces a problem, using the built-in versioning capability of VM Templates in Content Libraries. Which workflow should be used?

A) Check out the VM template to create an editable VM, make changes, then check it back in to create a new version
B) Convert the template to a VM, edit it, and convert it back to a template with a new name
C) Clone the template into a second Content Library as a manual backup before editing
D) Enable publish/subscribe replication so the subscribed library automatically retains old copies

---

**Q29.** An administrator needs to migrate a powered-on VM using cross vCenter vMotion from vCenter Server A to vCenter Server B. The two vCenter Server instances are registered in different SSO domains and are not linked. Which method allows this migration to complete?

A) It cannot be done; cross vCenter vMotion requires both vCenter Servers to share the same SSO domain
B) Drag and drop the VM between the two vCenter Server inventories in the vSphere Client
C) Use PowerCLI's Move-VM cmdlet, supplying separate credentials for the source and destination vCenter Servers
D) Temporarily join both vCenter Servers to Enhanced Linked Mode, perform the migration, then unlink them

---

**Q30.** What is the maximum virtual machine hardware (compatibility) version supported when a VM is running on an ESXi 8.0 host?

A) Version 17
B) Version 19
C) Version 21
D) Version 20

---

**Q31.** A VM displays a configuration issue in vCenter stating that disk consolidation is needed, after a third-party backup job failed to remove snapshot delta files correctly. Delta disks have been accumulating for several days. Which action resolves this without causing data loss?

A) Revert the VM to its most recent snapshot to discard the deltas
B) Delete all snapshots from Snapshot Manager and reboot the VM
C) Power off the VM and manually delete the delta VMDK files from the datastore
D) Right-click the VM, select Snapshots, and run Consolidate

---

**Q32.** A VM includes a Raw Device Mapping (RDM) configured in physical compatibility mode, used to support an MSCS cluster across physical hosts. The administrator performs a Storage vMotion on this VM to move it to a new datastore. What happens to the RDM's underlying LUN during this operation?

A) The RDM mapping file is migrated to the destination datastore; the data on the underlying physical LUN is not moved
B) The RDM is automatically converted to a standard VMDK on the destination datastore
C) Storage vMotion fails immediately because VMs with any RDM cannot be migrated
D) Both the RDM mapping file and the physical LUN's data are copied to the destination datastore

---

**Q33.** An administrator attempts to export a VM protected by VM Encryption as an OVF template for archival purposes. What must be done before this export can succeed?

A) Nothing; OVF export natively supports encrypted VMs without any prerequisite steps
B) A vSphere Trust Authority attestation token must be generated and attached to the export job
C) The VM must be decrypted before exporting, since OVF export does not support encrypted virtual machines
D) The VM's encryption must be converted to use a virtual TPM (vTPM) instead of VM Encryption before export

---

**Q34.** A remote office administrator configures a subscribed content library that points to a published library located at headquarters, connected over a slow, metered WAN link. The team wants templates and OVF templates to appear in the library catalog for browsing and rapid deployment, but wants to avoid consuming local datastore capacity and WAN bandwidth until an item is actually deployed. Which subscribed library configuration meets this requirement?

A) Configure the subscribed library to 'Download content immediately' so all items are always ready to deploy
B) Configure the subscribed library to 'Download content when needed' so only metadata syncs until an item is deployed
C) Configure the library as a second published library and manually sync items on a schedule
D) Disable automatic sync and use OVF export/import manually whenever a new template is added

---

**Q35.** A VM has been running for several weeks with an active snapshot taken before a failed patch attempt. An administrator selects 'Delete All' from the Snapshot Manager, but a subsequent storage report shows the VM still has multiple delta disk files consuming space, and the vSphere Client displays a warning icon on the VM stating that snapshot consolidation is needed. What should the administrator do?

A) Manually browse the datastore and delete the -delta.vmdk files associated with the VM
B) Power off the VM and clone it to a new VM to force the base disks to merge
C) Right-click the VM and select the 'Consolidate' option to merge the redundant delta disks into the base disk
D) Restart the hostd management agent on the ESXi host running the VM

---

**Q36.** An administrator enables Enhanced vMotion Compatibility (EVC) on a cluster containing hosts with mixed generations of Intel Xeon CPUs, selecting a baseline that both host generations support. Several VMs in the cluster were already powered on before EVC was enabled. What must happen before those already-running VMs are constrained to the new EVC CPU feature baseline?

A) The VMs must be vMotioned to a different host within the same cluster
B) The VMs must be powered off and then powered back on
C) The VM's CPU/MMU virtualization setting must be manually changed from Automatic to Hardware
D) The cluster must be placed into and then taken out of Maintenance Mode

---

**Q37.** You have a resource pool named 'Finance-RP' configured with a Memory reservation of 16 GB and Expandable Reservation enabled. VMs already running inside the pool consume the full 16 GB in reservations. An administrator attempts to power on an additional VM configured with a 4 GB memory reservation. The parent resource pool currently has 32 GB of unreserved memory available. What happens when the VM is powered on?

A) The power-on operation fails with insufficient resources because Finance-RP's reservation is fixed at 16 GB and cannot exceed its configured value.
B) The power-on operation succeeds because Finance-RP borrows the additional 4 GB reservation from its parent resource pool.
C) vCenter Server automatically and permanently increases Finance-RP's configured reservation to 20 GB to accommodate the VM.
D) The VM powers on but is placed in an unreserved state, causing memory contention for all VMs already running in the pool.

---

**Q38.** A vSphere HA cluster contains 8 identical ESXi hosts, each with 128 GB of physical memory. The cluster's admission control policy is set to 'Cluster resource percentage' with both CPU and memory failover capacity set to 25%. Ignoring virtualization overhead, what is the maximum amount of memory available for powered-on VM reservations in this cluster?

A) 1024 GB — the full physical memory capacity of the cluster
B) 256 GB — the amount of memory set aside for the failover capacity itself
C) 896 GB — capacity remaining after subtracting one host's worth of memory (128 GB)
D) 768 GB — capacity remaining after subtracting the 25% reserved failover capacity from the cluster total

---

**Q39.** An administrator creates a VM/Host affinity rule of type 'Must run on hosts in group' that binds a group of database VMs to a host group containing only Host-A and Host-B. DRS is disabled in this cluster. Host-A fails unexpectedly, and Host-B currently has no free resources available for the affected VMs. vSphere HA attempts to restart the failed VMs. What is the outcome?

A) HA restarts the VMs on Host-B using DRS to evict lower-priority VMs and free the required capacity.
B) HA restarts the VMs on any available host in the cluster, temporarily overriding the affinity rule until DRS can relocate them.
C) HA restarts the VMs on Host-B anyway, oversubscribing its memory, since HA always overrides resource limits during a failover event.
D) HA cannot restart the VMs, because the 'must run on' rule is mandatory and hard-enforced, restricting placement strictly to the specified host group regardless of available capacity elsewhere.

---

**Q40.** In vSphere 8, what is the maximum number of vCPUs supported for a single virtual machine protected by vSphere Fault Tolerance?

A) 4 vCPUs — this has been the fixed maximum since vSphere Fault Tolerance was introduced
B) 2 vCPUs — FT only supports single-threaded workloads to guarantee lockstep
C) 16 vCPUs — matching the maximum supported by vSphere HA admission control slot sizing
D) 8 vCPUs — the current supported maximum for an FT-protected VM

---

**Q41.** What is the default 'APD timeout' value in vSphere HA before an ESXi host formally declares a datastore to be in an All Paths Down (APD) state, potentially triggering the configured HA APD response?

A) 60 seconds
B) 140 seconds — the fixed default value after which the host declares the device to be in an APD state
C) 180 seconds — the same value commonly associated with the 'conservative' VM restart delay used in PDL responses
D) 300 seconds

---

**Q42.** A cluster contains two top-level resource pools: 'RP-Gold' configured with High CPU shares, and 'RP-Silver' configured with Normal CPU shares. Inside RP-Silver, a VM named 'Web-01' is individually configured with Custom CPU shares set to a very high numeric value (10,000). During CPU contention, how does DRS treat Web-01 relative to VMs residing directly inside RP-Gold?

A) Web-01 receives higher CPU priority than VMs in RP-Gold, because its custom share value (10,000) numerically exceeds RP-Gold's High setting.
B) Web-01's shares are compared only against sibling objects inside RP-Silver; its priority relative to RP-Gold is determined by RP-Silver's own pool-level share value, not Web-01's individual VM share value.
C) DRS ignores individual VM share values entirely once a VM resides inside any resource pool, defaulting every VM to Normal shares.
D) Web-01 automatically inherits RP-Gold's High share setting because its numeric share value is higher than the pool's default value.

---

**Q43.** A vSphere cluster has a parent resource pool named Production with an expandable CPU reservation of 20 GHz. Two child resource pools exist under it: Pool-A (CPU reservation 8 GHz, expandable enabled) and Pool-B (CPU reservation 8 GHz, expandable enabled). During heavy contention, Pool-A repeatedly reserves CPU capacity beyond its configured 8 GHz by borrowing unreserved capacity from Production, leaving Pool-B unable to power on new VMs because insufficient reservation capacity remains. Which change corrects this while preserving Pool-B's guaranteed minimum?

A) Increase the shares value on Pool-B to High so it receives more CPU during contention
B) Increase Pool-B's reservation to 12 GHz to match Pool-A's actual consumption
C) Set a CPU limit on Pool-B equal to its reservation to guarantee its allocation
D) Disable expandable reservation on Pool-A so it can only draw on its own configured 8 GHz reservation

---

**Q44.** An 8-host vSphere HA cluster uses the 'Cluster resource percentage' admission control policy with automatic percentage calculation based on 1 host failure. The administrator wants HA to issue a warning if VM performance after a failover would be degraded beyond an acceptable threshold, without blocking VM power-on. Which additional admission control setting achieves this?

A) Slot size policy with a fixed CPU/memory slot size
B) Host failures cluster tolerates, set under the slot-based policy
C) Performance degradation VMs tolerate, expressed as a percentage
D) Dedicated failover hosts specifying two reserved hosts

---

**Q45.** A business-critical VM configured with 6 vCPUs and 32 GB RAM must be protected against unplanned host failure with zero downtime and zero data loss. The architect wants to enable vSphere Fault Tolerance to meet this requirement. Which statement correctly describes what must be done before FT can be enabled on this VM?

A) FT can be enabled immediately since HA is already running in the cluster
B) The VM must first be migrated to a resource pool with an unlimited CPU reservation
C) The VM must first be reduced to 4 or fewer vCPUs, the maximum supported for FT-protected VMs
D) The VM must first be converted to use Storage vMotion-compatible thin disks

---

**Q46.** A business-critical VM configured with 8 vCPUs runs on a heavily consolidated ESXi host. Users report intermittent slowness. In esxtop's CPU view, the VM's %RDY value is consistently above 1000 (roughly 12-15% per vCPU), while %USED is low. Which action BEST resolves the root cause of this performance issue?

A) Increase the VM's CPU limit to guarantee more MHz
B) Reduce the VM's vCPU count to match its actual workload, easing physical CPU scheduling contention
C) Enable CPU Hot Add on the VM so more vCPUs can be added later
D) Migrate the VM to a host with faster clock speed without checking cluster-wide CPU overcommitment

---

**Q47.** An organization requires that the vCenter Server Machine SSL certificate be signed by their internal corporate CA for compliance, but wants to continue using VMCA to automatically issue and manage all ESXi host certificates with minimal administrative overhead. Which approach satisfies both requirements?

A) Switch the entire environment to Custom Certificate Authority mode so all certificates, including ESXi hosts, are replaced
B) Configure VECS to operate in thumbprint mode for the affected vCenter Server
C) Regenerate the VMCA root certificate using the corporate CA's public key
D) Use vSphere Certificate Manager to replace only the Machine SSL certificate with a certificate signed by the corporate CA, leaving VMCA as the CA for ESXi host certificates

---

**Q48.** Before remediating a vLCM cluster-level image to a newer ESXi version, an administrator wants to verify that all host firmware and driver combinations reported by the vendor's Hardware Support Manager are compatible with the target image. Which vLCM feature provides this validation?

A) Baseline compliance scan
B) Quick Boot compatibility check
C) Image depot export validation
D) Hardware compatibility check

---

**Q49.** An administrator enables Strict Lockdown Mode on an ESXi host that is managed by vCenter Server. What is the resulting behavior regarding the Direct Console User Interface (DCUI)?

A) The DCUI remains available only to users on the Exception Users list
B) The DCUI service is stopped, and the host can only be managed through vCenter Server
C) SSH is automatically enabled to provide an alternate management path
D) The root account retains full local DCUI login access for emergency use

---

**Q50.** A vSphere administrator assigns a user the 'Virtual Machine Power User' role directly on a VM folder object but leaves the 'Propagate to children' checkbox unchecked. What effect does this have on the VMs contained within that folder?

A) The user has no permissions on the VMs inside the folder because the role was not propagated
B) The user automatically receives Administrator rights on the VMs
C) The user receives read-only access to the VMs by default
D) Propagation only matters when the permission is assigned at the vCenter Server root object

---

**Q51.** While troubleshooting slow VM disk I/O, an administrator runs esxtop and observes for a datastore device: GAVG/cmd = 45ms, DAVG/cmd = 40ms, KAVG/cmd = 5ms. What does this data indicate about where the latency is occurring?

A) The physical storage array or backend device is the primary source of latency
B) The VMkernel storage stack is queuing commands excessively
C) Network latency between vSAN cluster nodes is the cause
D) HBA queue depth misconfiguration is causing kernel-level queuing delays

---

**Q52.** An ESXi 8.0 host is part of a cluster managed by a single vSphere Lifecycle Manager (vLCM) image that includes a firmware-and-drivers add-on supplied by the server vendor's Hardware Support Manager (HSM) plugin. Remediation fails on this host with an error stating that the HSM cannot reach the host's baseboard management controller (BMC) to apply firmware updates. Every other host in the cluster remediates successfully. What is the MOST likely cause?

A) The image contains a component that is incompatible with ESXi Quick Boot
B) The cluster's EVC mode does not support firmware-level remediation
C) vLCM requires the host to be removed from the cluster before firmware can be updated
D) The host's BMC (e.g., iDRAC/iLO) network credentials or connectivity registered with the Hardware Support Manager are incorrect or unreachable

---

**Q53.** An administrator suspects CPU scheduling contention for a wide 8-vCPU VM on a host running several other vCPU-heavy VMs competing for physical cores. In the esxtop CPU panel, which counter specifically indicates the percentage of time the VM's vCPUs were ready to run but held back because all of the VM's vCPUs could not be scheduled together on physical cores at the same time?

A) %CSTP
B) %RDY
C) %SWPWT
D) %MLMTD

---

**Q54.** A company's security policy requires that the vCenter Server Machine SSL certificate be issued by their internal enterprise CA, while all solution user certificates continue to be automatically signed and renewed by VMCA to minimize operational overhead. Which VMCA certificate management mode should the administrator configure to meet this exact requirement?

A) Full custom certificate mode
B) Thumbprint mode
C) VMCA as a subordinate (intermediate) CA of the enterprise root
D) Hybrid mode

---

