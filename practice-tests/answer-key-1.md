# Answer Key — Practice Test 1

**Q1. Correct: D**

Large supports up to 1,000 hosts and 10,000 VMs, which comfortably covers 350 hosts and, critically, the 4,500 VM count that exceeds Medium's 4,000 VM ceiling.

---

**Q2. Correct: B**

VAMI, accessed at https://<vcsa-fqdn-or-ip>:5480, is the dedicated appliance management portal for NTP, network settings, disk space monitoring, backup, and patching of the vCenter Server Appliance itself.

---

**Q3. Correct: C**

Starting with ESXi 7.0 and continuing in ESXi 8.0, the installer consolidates the boot bank, scratch, locker, and core dump areas into a single ESX-OSData volume, simplifying the disk layout and improving support for smaller boot devices.

---

**Q4. Correct: D**

Enhanced Linked Mode joins multiple vCenter Server instances to the same SSO domain, providing a unified inventory view, shared roles/permissions/licensing, and enabling cross-vCenter operations like vMotion from one vSphere Client session.

---

**Q5. Correct: C**

The vSphere 8 configuration maximums specify 96 ESXi hosts as the maximum supported per HA/DRS cluster, a limit that has remained consistent since vSphere 7.

---

**Q6. Correct: B**

The ks= kernel boot option tells the ESXi installer where to find the kickstart script (e.g., ks=http://server/ks.cfg, ks=usb, or ks=cdrom:/ks.cfg), enabling fully scripted, unattended installations.

---

**Q7. Correct: A**

The Large vCenter Server Appliance size officially supports up to 1,000 hosts and 10,000 VMs, comfortably covering 500 hosts and 5,000 VMs with headroom for growth.

---

**Q8. Correct: C**

Auto Deploy provisions ESXi hosts over the network at boot time using a designated image profile, loading the hypervisor into memory without requiring a local installation — the definition of stateless deployment.

---

**Q9. Correct: C**

The VAMI (Virtual Appliance Management Interface) for vCenter Server Appliance is accessed over HTTPS on port 5480 by default, used for appliance-level administration such as patching, backup, and health monitoring.

---

**Q10. Correct: C**

Route based on physical NIC load (Load Based Teaming, LBT) is available only on a vDS and dynamically moves flows between uplinks when one uplink's utilization exceeds 75% for 30 seconds, achieving true load-aware distribution.

---

**Q11. Correct: D**

Network I/O Control (NIOC) version 3 on a vDS allows administrators to set bandwidth reservations, shares, and limits per system traffic type (such as vMotion). A reservation guarantees minimum bandwidth only during contention, while allowing full link usage when the network is not congested.

---

**Q12. Correct: A**

vSAN traffic requires a VMkernel adapter with the vSAN traffic service explicitly enabled; without it, hosts cannot communicate for object placement, resynchronization, and cluster heartbeat traffic.

---

**Q13. Correct: D**

LACP (dynamic link aggregation using LACP protocol between the vDS and physical switch) is a distributed switch-only feature configured through a Link Aggregation Group (LAG); standard switches do not support LACP.

---

**Q14. Correct: D**

Setting the port group VLAN ID to 4095 enables Virtual Guest Tagging (VGT) mode, which passes all VLAN tags through to the guest OS unmodified, allowing the nested hypervisor to handle VLAN tagging itself.

---

**Q15. Correct: A**

Explicit failover order lets the administrator define exactly which uplink is active and which is standby; traffic only fails over to the standby uplink upon failure of the active one and does not load balance across both simultaneously.

---

**Q16. Correct: A**

Route based on physical NIC load, also known as Load Based Teaming (LBT), is available only on a vSphere Distributed Switch and periodically checks uplink utilization (every 30 seconds), remapping virtual ports to different physical uplinks when load exceeds 75% utilization on any uplink. This dynamically balances traffic based on actual load rather than a static algorithm.

---

**Q17. Correct: C**

Bandwidth reservation in NIOC v3 guarantees a minimum amount of bandwidth to a system traffic type or VM, and that reserved bandwidth is available even during contention, while still allowing the traffic type to burst above the reservation when spare capacity exists on the uplink.

---

**Q18. Correct: B**

vSphere provides a dedicated vMotion TCP/IP stack that has its own routing table, default gateway, and DNS configuration, isolated from the default (management) TCP/IP stack. Selecting this stack when creating the VMkernel adapter ensures vMotion traffic is routed independently of management traffic.

---

**Q19. Correct: B**

Round Robin cycles I/O across all active optimized paths in a configurable batch, providing load distribution across paths on ALUA-capable active-active arrays.

---

**Q20. Correct: A**

vSAN ESA uses a single storage pool per host built from high-performance NVMe/flash devices, eliminating the separate cache/capacity tier split required by OSA and providing better space efficiency through compression and native snapshots.

---

**Q21. Correct: B**

RAID-5 erasure coding with FTT=1 requires a minimum of 4 hosts, consuming less raw capacity than RAID-1 mirroring while still tolerating one failure.

---

**Q22. Correct: A**

vVols map individual VM objects, including disks, snapshots, and clones, directly to storage array objects via a VASA provider, allowing array-based data services to be applied per-VM while vCenter retains per-VM control instead of managing one large LUN as a single container.

---

**Q23. Correct: C**

NFS 4.1 in vSphere supports native multipathing through session trunking, allowing multiple network connections to a single NFS server without depending on link aggregation, a capability NFS 3 lacks.

---

**Q24. Correct: B**

When an array explicitly returns SCSI sense codes indicating a device is permanently gone, this is a Permanent Device Loss (PDL) condition; VMCP, part of vSphere HA, can be configured to automatically power off and restart affected VMs on hosts that still have access to storage.

---

**Q25. Correct: C**

RAID-5 erasure coding with FTT=1 requires a minimum of 4 hosts (3 data components + 1 parity component) in an all-flash vSAN cluster. This is a hard requirement enforced by SPBM compliance checks.

---

**Q26. Correct: B**

The Protocol Endpoint (PE) is the access point / I/O proxy that ESXi hosts use to communicate with the storage array for all vVol data operations (read/write I/O), eliminating the need for per-VM LUNs.

---

**Q27. Correct: A**

Most Recently Used (VMW_PSP_MRU) is the recommended and typically default PSP for active-passive arrays without ALUA. It continues using the last active path until it fails, avoiding the path flapping/thrashing that Fixed can cause when multiple hosts fight over which path is 'preferred'.

---

**Q28. Correct: C**

When snapshot delta files remain on disk but the Snapshot Manager shows none (often after a failed snapshot removal), vSphere flags the VM as needing consolidation. The Consolidate operation merges orphaned delta disks into the base disk while the VM continues running, without needing to recreate a snapshot first.

---

**Q29. Correct: D**

A published content library at the central site combined with subscribed libraries at remote sites allows scheduled or on-demand synchronization, controlling WAN bandwidth usage and ensuring remote sites have updated templates and ISOs without manual copying.

---

**Q30. Correct: C**

vSphere 8.0 introduces virtual hardware version 20, which is required to expose the newest ESXi 8.0 host features to the guest VM, including the latest virtual device and PMem enhancements.

---

**Q31. Correct: D**

OVA (Open Virtualization Appliance) is simply an OVF package packaged as a single tar archive containing the .ovf descriptor, .mf manifest, and disk files, making it easier to distribute as one file, whereas OVF distributes these as separate files.

---

**Q32. Correct: D**

Storage vMotion relocates a running VM's virtual disk files between datastores with no downtime, which is exactly what is needed to evacuate VM data from a datastore entering maintenance mode.

---

**Q33. Correct: B**

EVC masks CPU features so that all hosts in a cluster present a common baseline instruction set, allowing live vMotion of running VMs between hosts with different CPU generations without triggering CPU incompatibility errors.

---

**Q34. Correct: B**

A published content library replicates items to any subscribed library. Setting the subscribed library to download content immediately (rather than on-demand) ensures a full local copy exists at the branch site, satisfying offline availability even during WAN outages.

---

**Q35. Correct: B**

vSphere supports a hard maximum of 32 snapshots in a single snapshot chain per VM. VMware best practice, however, recommends keeping no more than 2-3 snapshots and removing them within 24-72 hours to avoid performance degradation.

---

**Q36. Correct: C**

For a physical compatibility mode RDM, Storage vMotion can move the VM home files and the small RDM mapping file to a new datastore, but the actual LUN data is never migrated -- the VM continues to access the raw LUN directly, preserving the pass-through behavior clusters depend on.

---

**Q37. Correct: A**

When 'Expandable Reservation' is disabled, a resource pool cannot borrow unreserved resources from its parent (or the cluster) even if capacity exists above it. Admission control for the VM's power-on evaluates only against the resource pool's own defined reservation, so the operation fails with an insufficient resources error.

---

**Q38. Correct: A**

Partially Automated mode has DRS automatically place VMs at power-on, but all load-balancing migration recommendations after that must be manually approved by an administrator before they execute — matching the requirement that placement is automatic but every vMotion still needs explicit human approval.

---

**Q39. Correct: A**

With the percentage-based admission control policy, the administrator directly specifies the percentage of total cluster CPU and memory resources set aside as reserved failover capacity. At 25% in a 4-host cluster this happens to be numerically similar to one host, but the setting itself reserves a percentage of the aggregate pool, not a specific host count.

---

**Q40. Correct: B**

vSphere Fault Tolerance supports symmetric multiprocessor (SMP-FT) protected VMs with up to 8 vCPUs per FT-protected virtual machine in vSphere 8 with Enterprise Plus licensing.

---

**Q41. Correct: B**

Datastore heartbeating allows HA master hosts to check whether an isolated host is still alive and updating heartbeat files on shared datastores. If datastore heartbeats are present, HA concludes the host is isolated (not dead) and, depending on the configured isolation response, can leave the VMs running rather than triggering unnecessary failovers.

---

**Q42. Correct: A**

vSphere's default predefined share levels use a 4:2:1 ratio, meaning a VM or resource pool set to High receives twice the shares of one set to Normal, and four times the shares of one set to Low, proportionally influencing contention-based allocation.

---

**Q43. Correct: D**

Shares assigned to a resource pool determine that pool's proportional entitlement to the parent's resources as a single entity (default pool-level CPU share ratio is High:Normal:Low = 8000:4000:2000, a 2:1 ratio for High vs Normal). The number of VMs inside a pool does not change the pool's own share weight; each pool then subdivides its allocation among its own children.

---

**Q44. Correct: D**

When automatic calculation is used with the Cluster resource percentage policy and hosts are of equal size, vSphere HA computes the reserved percentage as (1 / number of hosts) x 100. With 1 failure to tolerate and 4 hosts, that is 1/4 = 25%.

---

**Q45. Correct: C**

vSphere Fault Tolerance (SMP-FT) supports protected virtual machines with up to 8 vCPUs, provided the appropriate licensing edition, compatible hardware version, and host CPU support are in place.

---

**Q46. Correct: C**

vLCM cluster images support vendor add-ons that bundle firmware and drivers for specific hardware. Adding the correct add-on to the image and remediating ensures the host receives the required driver while keeping the entire cluster on a single, consistent image.

---

**Q47. Correct: D**

%RDY represents the percentage of time a vCPU was ready to run but had to wait in the queue for a physical CPU to be scheduled. A value above roughly 10% is generally considered a sign of CPU contention on the host.

---

**Q48. Correct: D**

In VMCA subordinate CA mode, VMCA's own certificate is signed by the enterprise CA, establishing a trusted chain, while VMCA continues to automatically issue and manage certificates for ESXi hosts and solution users, satisfying both requirements.

---

**Q49. Correct: B**

In the vSphere permission model, an explicit permission assigned directly on an object always takes precedence over an inherited permission propagated from a parent object, regardless of whether propagation was enabled on the parent assignment.

---

**Q50. Correct: D**

VECS is the local certificate store present on each vCenter Server node that holds the SSL certificates, private keys, and trusted CA certificates used by vCenter services and solution users.

---

**Q51. Correct: B**

DAVG measures the average latency at the device driver level — the time it takes commands to complete against the physical storage device. High DAVG combined with near-zero KAVG (VMkernel queuing latency) points to the physical storage array or SAN fabric as the source of the delay, since the ESXi host itself is not queuing commands.

---

**Q52. Correct: A**

vLCM cluster images support attaching a Hardware Support Manager (provided by the server vendor, e.g., via OEM.com integration) so firmware and driver updates are validated and applied together with the ESXi image as a single desired state.

---

**Q53. Correct: A**

A sustained %RDY above roughly 10% per vCPU indicates the VM is frequently waiting for physical CPU scheduling and is a commonly cited threshold for CPU contention investigation in vSphere performance troubleshooting.

---

**Q54. Correct: A**

Assigning the role at the specific VM folder with propagation enabled scopes the permission to only that folder's contents (including current and future VMs) without affecting other datacenters or folders.

---

