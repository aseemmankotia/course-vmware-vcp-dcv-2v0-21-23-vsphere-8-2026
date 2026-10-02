# Practice Test 1: VCP-DCV 2V0-21.23: vSphere 8 Exam-Focused Prep

- **Questions:** 54
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-1.md`. Track results in `score-tracker.md`.

---

**Q1.** An architect is sizing a new vCenter Server Appliance deployment for an environment that currently has 350 ESXi hosts and is expected to grow to 4,500 powered-on VMs within the year. Which deployment size BEST meets these requirements while avoiding unnecessary resource overhead?

A) Small (up to 100 hosts / 1,000 VMs)
B) Medium (up to 400 hosts / 4,000 VMs)
C) X-Large (up to 2,000 hosts / 35,000 VMs)
D) Large (up to 1,000 hosts / 10,000 VMs)

---

**Q2.** Which vCenter Server Appliance interface is used to configure appliance-level settings such as NTP time sync, network configuration, and applying appliance patches?

A) ESXi Host Client
B) VMware Appliance Management Interface (VAMI)
C) vSphere Client
D) PowerCLI Get-VMHost cmdlet

---

**Q3.** When installing ESXi 8.0 on a supported boot device, which new partition/volume replaces the legacy scratch, locker, and core dump partitions used in older ESXi versions?

A) A dedicated VMFS-L locker partition
B) An Auto Deploy cache partition
C) The ESX-OSData volume
D) A standard VMFS6 datastore partition

---

**Q4.** A company runs two separate vCenter Server instances in different data centers and wants administrators to view and manage both inventories from a single vSphere Client session, including cross-vCenter vMotion. Both vCenters are joined to the same SSO domain. What is this configuration called?

A) Cross vCenter High Availability
B) Hybrid Linked Mode
C) Federated vCenter Topology
D) Enhanced Linked Mode

---

**Q5.** An architect is designing a vSphere 8 cluster and must confirm the maximum number of ESXi hosts that can be placed into a single vSphere HA/DRS cluster.

A) 32 hosts
B) 64 hosts
C) 96 hosts
D) 128 hosts

---

**Q6.** During a scripted, unattended ESXi 8 installation, the installer needs to locate the kickstart configuration file that defines partitioning, network, and root password settings. Which boot option is used to specify the location of this file?

A) bootproto=dhcp in the boot.cfg file
B) ks= boot option pointing to the installation script location
C) vmkernel.boot=auto in the BIOS setup
D) autodeploy.cfg referenced from vCenter

---

**Q7.** An architecture team is sizing a new vCenter Server Appliance deployment for a single vCenter Server instance that will manage 500 ESXi hosts and 5,000 virtual machines, with room to grow slightly. Which vCenter Server Appliance deployment size BEST meets these requirements?

A) Large (up to 1,000 hosts / 10,000 VMs)
B) Medium (up to 400 hosts / 4,000 VMs)
C) Small (up to 100 hosts / 1,000 VMs)
D) Tiny (up to 10 hosts / 100 VMs)

---

**Q8.** A company plans to provision 200 new ESXi 8.0 hosts as stateless nodes that boot their hypervisor image over the network from a central image profile, with no ESXi installation persisted to local disk. Which vSphere feature should be used to deploy these hosts?

A) Content Library
B) Host Profiles applied via vCenter
C) Auto Deploy
D) Interactive ISO installation with a kickstart file

---

**Q9.** An administrator needs to access the vCenter Server Appliance Management Interface (VAMI) to check appliance health and apply a patch. Which default TCP port must be used to reach this interface in a browser?

A) 443
B) 902
C) 5480
D) 9443

---

**Q10.** A vSphere administrator manages a vSphere Distributed Switch (vDS) with four physical uplinks. Several port groups experience uneven traffic patterns throughout the day, and the administrator wants traffic to be dynamically redistributed across uplinks based on actual physical NIC utilization rather than a static hash. Which NIC teaming and failover policy should be configured?

A) Route based on IP hash
B) Use explicit failover order
C) Route based on physical NIC load
D) Route based on originating virtual port

---

**Q11.** An administrator must guarantee that vMotion traffic receives a minimum amount of bandwidth on shared 10GbE uplinks during periods of network contention, without permanently limiting other traffic types when the network is idle. Which vSphere Distributed Switch feature should be used?

A) Configure a traffic shaping policy on the vMotion port group
B) Assign a dedicated VLAN ID to the vMotion VMkernel port group
C) Enable promiscuous mode on the vMotion port group
D) Enable Network I/O Control and set a bandwidth reservation for the vMotion system traffic type

---

**Q12.** A VMkernel adapter on an ESXi 8 host needs to carry vSAN traffic between hosts in a vSAN cluster. Which service must be enabled on that VMkernel adapter?

A) vSAN
B) Management
C) Provisioning
D) vMotion

---

**Q13.** Which networking feature requires a vSphere Distributed Switch and is NOT available on a vSphere Standard Switch?

A) VLAN tagging on a port group
B) NIC teaming with multiple uplinks
C) Promiscuous mode security policy
D) LACP dynamic link aggregation

---

**Q14.** An administrator is setting up a nested ESXi lab where a VM running ESXi must send and receive traffic tagged with multiple VLAN IDs through a single vNIC connected to a vDS port group. Which VLAN ID should be set on the port group to enable VLAN trunking so all VLANs pass through untouched to the guest?

A) 1
B) 0
C) 4094
D) 4095

---

**Q15.** A security team requires that a specific VM port group always use one designated uplink as active, with a second uplink used only if the primary fails, and traffic must never automatically shift back to load-balance across both uplinks simultaneously. Which teaming and failover configuration meets this requirement?

A) Use explicit failover order with one uplink set as active and the other as standby
B) Route based on IP hash with both uplinks active
C) Route based on originating virtual port with both uplinks active
D) Route based on physical NIC load with both uplinks active

---

**Q16.** A vSphere 8 cluster uses a distributed switch backed by four 25GbE uplinks. Administrators notice that VM traffic is unevenly distributed across the uplinks even though overall utilization is low, and they want traffic dynamically rebalanced based on actual physical NIC load rather than a static hash. Which NIC teaming and failover policy should be configured on the port group to BEST meet this requirement?

A) Route based on physical NIC load (LBT)
B) Route based on originating virtual port
C) Route based on IP hash
D) Use explicit failover order

---

**Q17.** A company enables Network I/O Control (NIOC) version 3 on a distributed switch and wants to guarantee that the vMotion traffic type always receives at least 2 Gbps of bandwidth during periods of contention, without imposing a hard ceiling on it when bandwidth is available. Which NIOC construct should be used to meet this requirement?

A) Configure a limit of 2 Gbps on the vMotion traffic type
B) Increase the shares value for the vMotion traffic type to a custom high value
C) Configure a bandwidth reservation of 2 Gbps on the vMotion traffic type
D) Move vMotion to its own dedicated physical uplink outside NIOC

---

**Q18.** An administrator needs to create a VMkernel adapter on an ESXi 8.0 host that will be used exclusively for vMotion traffic and must be isolated from management traffic at the TCP/IP stack level so that vMotion uses its own default gateway and routing table. Which action accomplishes this?

A) Enable only the vMotion service on the VMkernel adapter using the default TCP/IP stack
B) Enable the vMotion TCP/IP stack when creating the VMkernel adapter and assign it to that adapter
C) Create the VMkernel adapter on a separate VLAN using the default TCP/IP stack
D) Assign the VMkernel adapter a static route using esxcli on the default TCP/IP stack

---

**Q19.** A company's vSphere 8 environment uses an active-active Fibre Channel array that supports ALUA. The storage team wants ESXi hosts to distribute I/O evenly across all available optimized paths to maximize throughput. Which Path Selection Policy should be configured on the affected datastores?

A) Fixed (VMW_PSP_FIXED)
B) Round Robin (VMW_PSP_RR)
C) Most Recently Used (VMW_PSP_MRU)
D) Adaptive Load Balancing (a generic native vSphere PSP)

---

**Q20.** An organization is designing a new all-flash vSAN 8 cluster and wants the simplest per-host storage architecture with a single pool of NVMe devices, no separate cache and capacity tiers, and improved space efficiency. Which vSAN architecture should they select?

A) vSAN Express Storage Architecture (ESA)
B) vSAN Original Storage Architecture (OSA) with all-flash disk groups
C) vSAN Original Storage Architecture (OSA) with hybrid disk groups
D) vSAN stretched cluster with fault domains

---

**Q21.** You are creating a vSAN storage policy that must tolerate one failure (FTT=1) using RAID-5 erasure coding to save capacity compared to mirroring. What is the minimum number of hosts contributing storage that the vSAN cluster must have to support this policy?

A) 3 hosts
B) 4 hosts
C) 5 hosts
D) 6 hosts

---

**Q22.** A company wants their storage array to natively manage per-VM snapshots, replication, and cloning policies while vCenter Server retains fine-grained visibility and control down to the individual virtual disk level, rather than treating the whole datastore as one large container. Which vSphere storage technology satisfies this requirement?

A) Virtual Volumes (vVols)
B) Traditional VMFS datastore on a single large LUN
C) NFS 4.1 datastore
D) vSAN datastore

---

**Q23.** Which feature is supported by NFS version 4.1 datastores in vSphere 8 but is NOT supported by NFS version 3 datastores?

A) Support for VAAI Full File Clone hardware offload
B) Ability to be used as a VM datastore
C) Multipathing through session trunking without requiring NIC teaming or LACP
D) Support for datastore heartbeating for HA

---

**Q24.** A LUN backing a datastore is deliberately unpresented from the storage array while several powered-on VMs still reside on it. The ESXi hosts immediately receive SCSI sense codes from the array confirming the device is permanently unavailable. Which condition is occurring, and which vSphere feature can automatically terminate and restart the affected VMs on healthy hosts?

A) All Paths Down (APD), handled by Storage I/O Control
B) Permanent Device Loss (PDL), handled by VM Component Protection (VMCP)
C) All Paths Down (APD), handled by VM Component Protection (VMCP)
D) Permanent Device Loss (PDL), handled by Storage DRS

---

**Q25.** An administrator configures a two-node vSAN cluster with a storage policy that has Failures to Tolerate (FTT) = 1 using RAID-5 erasure coding to save capacity. The cluster fails compliance checks and the objects remain non-compliant. What is the minimum number of hosts required in the vSAN cluster to support FTT=1 with RAID-5 erasure coding?

A) 3 hosts
B) 6 hosts
C) 4 hosts
D) 5 hosts

---

**Q26.** A company implements Virtual Volumes (vVols) on an array that supports VASA 3.0. VM data operations such as read and write I/O must pass through a specific logical I/O proxy on the ESXi host rather than requiring a traditional LUN to be provisioned per VM. Which vVols component performs this function?

A) VASA Provider
B) Protocol Endpoint
C) Storage Container
D) Config-VVol

---

**Q27.** An ESXi host connects to a storage array in an active-passive configuration without ALUA support. Administrators notice frequent path thrashing between two hosts accessing the same LUN when using the Fixed path selection policy. Which native multipathing (PSP) policy should be configured to eliminate this path thrashing?

A) VMW_PSP_MRU
B) VMW_PSP_FIXED
C) VMW_SATP_ALUA
D) VMW_PSP_RR

---

**Q28.** A VM in vCenter Server shows no snapshots listed in the Snapshot Manager, but its datastore folder contains multiple delta VMDK files and the VM's disk usage keeps growing. Which action should the administrator take to resolve this without disrupting the VM's running state?

A) Delete the VM from inventory and re-register it
B) Power off the VM and manually delete the delta VMDK files from the datastore
C) Right-click the VM and select Consolidate to merge the redundant delta disks into the base disk
D) Migrate the VM to a new datastore using Storage vMotion to force disk cleanup

---

**Q29.** An organization has a central vCenter Server that maintains master copies of VM templates and ISO images. Multiple remote sites, each with their own vCenter Server and limited WAN bandwidth, need periodic access to updated templates. Which vSphere feature BEST meets this requirement?

A) vSphere Replication to each remote vCenter Server
B) Storage vMotion of templates to each remote datastore
C) Shared NFS datastore mounted by all remote vCenter Servers
D) A local content library at each site configured as a subscribed library with scheduled synchronization from the central published library

---

**Q30.** An administrator wants a virtual machine to have access to all VM hardware features supported by ESXi 8.0, including the latest virtual NVDIMM and PMem enhancements. Which virtual machine hardware version must the VM be configured with?

A) Version 17
B) Version 19
C) Version 20
D) Version 15

---

**Q31.** An administrator downloads a virtual appliance distributed as a single .ova file instead of a set of separate files. What does this indicate about the appliance package?

A) The OVA is a compressed VMDK-only archive that requires manual OVF descriptor creation before deployment
B) The OVA format is only compatible with Workstation and cannot be deployed to vCenter Server
C) The OVA file is an OVF template that has already been converted into a running VM
D) The OVA is a tar archive that bundles the OVF descriptor, manifest, and disk files into one file for easier distribution

---

**Q32.** A storage administrator needs to place a datastore into maintenance mode to perform firmware upgrades on the underlying array, but several powered-on VMs currently have virtual disks on that datastore. Which action allows the VMs to remain running while their disks are relocated off the affected datastore?

A) Enable Storage DRS in fully automated mode only after the maintenance window begins
B) Power off the VMs and use cold migration to move their files
C) Create a new snapshot for each VM and move only the snapshot files to a different datastore
D) Perform a Storage vMotion to move the VM disk files to a different datastore while the VM remains powered on

---

**Q33.** An administrator attempts to vMotion a running VM from a host with an Intel Skylake-generation CPU to a host with a newer Intel Ice Lake-generation CPU in the same cluster. The migration fails due to CPU incompatibility. Which cluster-level feature should be configured to allow vMotion between hosts with different CPU generations going forward?

A) Predictive DRS
B) Enhanced vMotion Compatibility (EVC), setting the cluster baseline to the lowest common CPU generation feature set
C) vSphere Cluster Services (vCLS)
D) Storage Policy Based Management (SPBM)

---

**Q34.** A company operates a primary vCenter Server at its headquarters and a secondary vCenter Server at a remote branch office connected by a WAN link. The administrator needs VM templates created at headquarters to automatically propagate to the branch office, with a full local copy stored there so the templates remain available for deployment even if the WAN link goes down. Which solution BEST meets this requirement?

A) Manually export each template to OVF and import it into the branch office vCenter inventory whenever it changes
B) Create a published content library at headquarters and configure a subscribed content library at the branch office with 'download content immediately' enabled
C) Place both vCenter Server instances in the same Single Sign-On domain with Enhanced Linked Mode so templates are automatically shared
D) Mount the same NFS datastore containing the templates to both vCenter Server instances across the WAN link

---

**Q35.** What is the maximum number of snapshots that vSphere 8 supports for a single virtual machine, regardless of the recommended best-practice limit?

A) 15 snapshots per VM
B) 32 snapshots per VM
C) 250 snapshots per VM
D) There is no fixed maximum; it is limited only by available datastore space

---

**Q36.** A powered-on virtual machine has a Raw Device Mapping (RDM) disk configured in physical compatibility mode, pointing to a LUN used for a clustered database. The administrator needs to perform a Storage vMotion to move the VM's configuration files to a different datastore for maintenance, without disrupting the physical compatibility RDM's direct LUN access. Which outcome should the administrator expect?

A) Storage vMotion is not supported at all when any RDM disk is present on the VM, in any compatibility mode
B) Storage vMotion will convert the physical compatibility mode RDM into a virtual disk (VMDK) automatically during the migration
C) Storage vMotion can relocate the VM's configuration files and the RDM mapping file to the new datastore, while the underlying LUN data itself remains in place and is still accessed directly
D) The VM must be powered off before Storage vMotion can proceed because physical mode RDMs block all live migrations

---

**Q37.** A resource pool named RP-Finance has a memory reservation of 16 GB with 'Reservation Not Expandable' selected. VMs inside RP-Finance are powered on and consume the full 16 GB. An administrator attempts to power on an additional VM inside RP-Finance that requires an additional 4 GB reservation, but there is 32 GB of unreserved memory available at the cluster level. What happens?

A) The power-on operation fails because RP-Finance cannot borrow reservation capacity from its parent
B) The VM powers on successfully because the cluster has sufficient unreserved capacity
C) The VM powers on but DRS automatically increases the resource pool reservation to 20 GB
D) The VM powers on in a degraded state with reduced memory allocation

---

**Q38.** A cluster hosts a mixed workload where administrators want vCenter to automatically calculate placement and migration recommendations for virtual machines, but a compliance policy requires that a human explicitly approve every vMotion before it executes. Which DRS automation level meets this requirement?

A) Partially Automated
B) Fully Automated
C) Manual
D) Disabled

---

**Q39.** An administrator configures vSphere HA admission control using the 'Cluster resource percentage' policy with a value manually set to 25% for both CPU and memory in a 4-host cluster where each host has identical capacity. What does this configuration guarantee?

A) 25% of the aggregate cluster CPU and memory capacity is reserved as failover capacity, independent of host count
B) Exactly one host's worth of capacity is reserved, equivalent to an N+1 policy
C) HA will tolerate the failure of 25% of the total number of virtual machines in the cluster
D) The cluster will power off 25% of running VMs if a host fails to conserve resources

---

**Q40.** What is the maximum number of vCPUs supported for a single virtual machine protected by vSphere Fault Tolerance in vSphere 8 with Enterprise Plus licensing?

A) 2 vCPUs
B) 8 vCPUs
C) 4 vCPUs
D) 16 vCPUs

---

**Q41.** A host in an HA-enabled cluster loses all management network heartbeat connectivity but retains full access to all shared datastores, and the VMs on that host continue running normally. Which HA feature allows the cluster to correctly determine that this is network isolation rather than a full host failure, avoiding an unnecessary restart of healthy VMs elsewhere?

A) Proactive HA
B) Datastore heartbeating
C) VM Component Protection (VMCP)
D) Admission control policy

---

**Q42.** By default, what is the CPU and memory shares ratio between the 'High', 'Normal', and 'Low' share levels on a resource pool or virtual machine in vSphere?

A) High:Normal:Low = 4:2:1
B) High:Normal:Low = 2:1:1
C) High:Normal:Low = 8:4:1
D) High:Normal:Low = 3:2:1

---

**Q43.** A cluster contains two resource pools created directly under the cluster root: RP-A configured with High CPU shares and containing 2 VMs, and RP-B configured with Normal CPU shares and containing 8 VMs. During CPU contention on the cluster, how will vSphere allocate CPU resources between RP-A and RP-B?

A) RP-B receives more CPU resources overall because it contains more VMs, so total demand from RP-B outweighs the share setting of RP-A
B) CPU is split equally between RP-A and RP-B because shares only affect siblings within the same resource pool, not resource pools competing against each other
C) Share values on resource pools are ignored by the scheduler; only reservations and limits determine how much CPU each pool receives during contention
D) RP-A as a whole pool receives twice the CPU allocation of RP-B based on the High vs Normal share ratio at the pool level; that allocation is then divided independently among each pool's own child VMs

---

**Q44.** A vSphere HA cluster contains 4 identically sized ESXi hosts. Admission control is enabled using the 'Cluster resource percentage' policy with Host failures the cluster tolerates set to 1, and the automatic percentage calculation is left enabled (not overridden). What percentage of cluster CPU and memory will HA reserve as failover capacity?

A) 50%
B) 33%
C) 10%
D) 25%

---

**Q45.** An administrator wants to protect a business-critical virtual machine using vSphere Fault Tolerance in a vSphere 8 environment. What is the maximum number of vCPUs supported on a single Fault Tolerance protected virtual machine?

A) 2 vCPUs
B) 4 vCPUs
C) 8 vCPUs
D) 16 vCPUs

---

**Q46.** An administrator manages a cluster with vSphere Lifecycle Manager (vLCM) using a single image. After adding a new host with a network adapter from a different vendor, the cluster image compliance check reports the new host as non-compliant due to a missing driver. Which action should the administrator take to bring the host into compliance?

A) Manually install the driver VIB on the host using esxcli and reboot the host
B) Remove the host from the cluster and manage it as a standalone host
C) Add the appropriate vendor add-on to the cluster image and remediate the cluster
D) Convert the cluster back to baseline-based Update Manager patching

---

**Q47.** A virtual machine exhibits sluggish performance despite low CPU utilization reported at the host level. Using esxtop, the administrator observes a %RDY value of 15 for one of the VM's vCPUs. What does this metric indicate?

A) The VM's guest OS is actively using 15% of its allocated CPU capacity
B) 15% of the VM's allocated memory has been reclaimed by the balloon driver
C) The host's physical CPU is running at only 15% of its rated clock speed
D) The vCPU spent 15% of the sample time waiting for a physical CPU to become available for scheduling

---

**Q48.** A company requires that all vCenter Server and ESXi certificates be signed by their internal enterprise Certificate Authority (CA), while still allowing vCenter Server itself to automatically issue and manage certificates for ESXi hosts and solution users. Which VMCA configuration mode should be used?

A) Full custom certificate mode with manually replaced certificates for every solution user
B) Default VMCA mode using a self-signed root certificate
C) Thumbprint mode for host and vCenter authentication
D) VMCA configured as a subordinate (intermediate) CA under the enterprise root CA

---

**Q49.** An administrator assigns a custom role to a user at the datacenter object with the 'Propagate to children' option enabled. Later, a different, more restrictive role is assigned directly to that same user on one specific virtual machine object, without enabling propagation on that assignment. What access will the user have on that virtual machine?

A) The combined (union) permissions of both the datacenter-level and VM-level roles
B) The permissions defined by the role assigned directly on the virtual machine object
C) The permissions from the datacenter-level role, since propagation always overrides child object assignments
D) No access at all, because the two conflicting role assignments cancel each other out

---

**Q50.** Which vCenter Server component is responsible for locally storing SSL certificates, private keys, and trusted root certificates used by vCenter Server services and solution users?

A) VMware Directory Service (vmdir)
B) The Single Sign-On (SSO) domain repository
C) The vSphere Client certificate cache
D) VMware Endpoint Certificate Store (VECS)

---

**Q51.** An administrator suspects a storage performance issue affecting a datastore. On the esxtop disk device screen, DAVG/cmd is consistently above 20ms while KAVG/cmd remains near 0. What does this pattern most likely indicate?

A) The ESXi VMkernel storage stack is the bottleneck, not the physical storage device
B) The latency is occurring at the physical storage array or SAN fabric level, outside the ESXi host
C) The virtual machine's guest OS is generating excessive I/O queue depth
D) Multipathing is misconfigured, causing path thrashing between storage paths

---

**Q52.** An organization manages a cluster of ESXi 8.0 hosts and wants a single desired-state specification that includes the ESXi base image, vendor add-ons, and automatic firmware updates coordinated with a server vendor's firmware update utility. Which vSphere Lifecycle Manager approach BEST meets this requirement?

A) Manage the cluster with a vLCM image and attach a Hardware Support Manager from the server vendor
B) Create baseline-based patching groups in the legacy Update Manager baseline workflow
C) Update ESXi hosts individually using esxcli software profile update commands
D) Sync a Content Library subscription containing the ESXi ISO to each host

---

**Q53.** While troubleshooting a performance issue with esxtop, an administrator observes the %RDY counter for a virtual machine's vCPUs. Sustained %RDY values above which threshold per vCPU are generally considered indicative of CPU contention that warrants investigation?

A) 10%
B) 50%
C) 1%
D) 90%

---

**Q54.** An administrator must grant a support team read-only access to all virtual machines contained within a single VM folder in one datacenter, without affecting other datacenters or folders in vCenter Server. How should the permission be configured?

A) Assign the Read-Only role on the specific VM folder with Propagate to children enabled
B) Assign the Read-Only role at the vCenter Server root with Propagate to children enabled
C) Assign the Read-Only role directly on each ESXi host in the cluster
D) Assign the Read-Only role on the specific VM folder with Propagate to children disabled

---

