# Answer Key — Practice Test 2

**Q1. Correct: B**

In VCHA, the Witness node is a minimal-footprint appliance whose only job is to provide quorum (tie-breaker) between the Active and Passive nodes to avoid split-brain scenarios. It does not hold a copy of the vCenter database.

---

**Q2. Correct: B**

VMware documents that Quick Boot, which skips the physical hardware BIOS/UEFI POST, is not compatible with hosts that have a physical TPM 2.0 chip because the TPM's platform configuration registers (PCRs) must be re-measured during a full hardware boot to maintain a valid trust chain; vLCM automatically falls back to a full reboot on such hosts.

---

**Q3. Correct: A**

The X-Large VCSA deployment size supports up to 2,000 hosts and 35,000 powered-on VMs, which is the only sizing tier that accommodates both the 2,000-host and 25,000-VM requirements.

---

**Q4. Correct: A**

Since vSphere 6.5/6.7's PSC-embedded architecture (carried into vSphere 7/8), Enhanced Linked Mode requires all participating vCenter Servers to share the same SSO domain. The cmsso-util move command lets you move an existing vCenter Server Appliance into another vCenter's SSO domain without redeploying it from scratch.

---

**Q5. Correct: C**

When a host has both UEFI Secure Boot enabled and a physical TPM 2.0 chip, ESXi can measure and seal boot component hashes into the TPM, and vCenter Server performs remote attestation, displaying the host's Secure Boot/attestation status on the host summary/monitor view as Passed or Failed.

---

**Q6. Correct: C**

The ESXi installer boot option 'ks=' specifies the URL or path where the kickstart (ks.cfg) configuration file is located, supporting protocols such as http, https, ftp, nfs, usb, and cdrom.

---

**Q7. Correct: B**

VMware deprecated booting ESXi 8.0 from SD cards/USB devices for hosting the ESX-OSData partition due to the high write-endurance demands of logs, scratch, and core dump data. Best practice is a persistent local storage device of at least 32GB, with 128GB or more recommended when running vSAN or storing extensive logs and core dumps.

---

**Q8. Correct: D**

vCenter HA requires a dedicated HA network, isolated on a separate VLAN/subnet from the management network, connecting the Active, Passive, and Witness nodes. Round-trip latency must be under 10ms to support the synchronous PostgreSQL replication between Active and Passive nodes.

---

**Q9. Correct: B**

Enhanced Linked Mode links up to 15 vCenter Server instances (vCenter Server Standard edition) that share a common SSO domain, giving administrators a single pane of glass to view, search, and manage inventory, roles, and licensing across all linked vCenter Servers.

---

**Q10. Correct: A**

NIOC v3 reservations guarantee a minimum amount of bandwidth to a traffic type that is enforced even under contention, and reserved bandwidth is subtracted from the pool available to other traffic types — this is the only mechanism that guarantees a floor rather than just a relative priority.

---

**Q11. Correct: C**

Ephemeral binding assigns ports on-demand and is the only binding type that allows a VM to be connected to a distributed port group directly through the ESXi host (via the host client or API) when vCenter Server is unavailable, since the port is created/removed dynamically without requiring vCenter to hold the assignment.

---

**Q12. Correct: B**

When using a LAG, the port group's failover order must specify the LAG itself as the active uplink (with standalone uplinks moved to unused); vSphere automatically applies 'Route based on IP hash' load balancing internally for LAG traffic, so the teaming policy option is greyed out and does not need to be manually selected.

---

**Q13. Correct: B**

A Community secondary PVLAN allows member ports to communicate with each other and with promiscuous ports (such as the gateway) on the primary VLAN, but not with ports in other secondary PVLANs (isolated or other community segments) — matching the stated requirement exactly.

---

**Q14. Correct: B**

vDS Health Check specifically validates VLAN trunking configuration, MTU consistency between the vDS and the connected physical switch ports, and teaming/failover configuration mismatches across each uplink — directly surfacing per-uplink MTU mismatches, which matches the symptom of a single uplink causing fragmentation.

---

**Q15. Correct: C**

VMware's documented multi-NIC vMotion design requires two separate port groups, each overriding the teaming/failover order so that one physical uplink is Active and the other is explicitly Unused (not Standby); each VMkernel adapter is then bound to a different port group, so each vMotion VMkernel interface deterministically uses a distinct uplink, enabling true parallel throughput across both NICs.

---

**Q16. Correct: D**

NIOC v3 admission control caps total reservable bandwidth for system traffic types at 75% of the aggregate physical NIC capacity by default (15 Gbps of 20 Gbps here). Adding 5 Gbps to the existing 11 Gbps reserved would total 16 Gbps, exceeding the quota, so the new reservation is rejected.

---

**Q17. Correct: A**

Creating a LAG object only defines the aggregation group; it does not automatically move traffic onto it. Each affected distributed port group's teaming and failover order must be manually edited so lag1 is Active and the standalone uplinks are set to Unused, forcing traffic onto the LAG.

---

**Q18. Correct: D**

VMware's documented multi-NIC vMotion configuration requires two separate VMkernel port groups, each with an explicit teaming/failover override so one uplink is active and the other unused per port group. This deterministically pins each vmkernel adapter to a distinct physical uplink. Placing both adapters on a single port group with default load balancing does not guarantee even uplink separation, which explains the observed underutilization.

---

**Q19. Correct: C**

vSphere 8 expanded VMFS6 automatic space reclamation priorities to None, Low, Medium, and High. High issues UNMAP commands most aggressively/fastest, reclaiming space quickest at the cost of more backend I/O.

---

**Q20. Correct: A**

For ALUA-capable arrays, VMware recommends Round Robin because it load-balances I/O across the active/optimized paths reported by the array while still respecting ALUA state, avoiding the thrashing risk that Fixed can cause on active/passive arrays.

---

**Q21. Correct: A**

RAID-6 erasure coding with FTT=2 requires 4 data segments plus 2 parity segments, needing a minimum of 6 hosts in the cluster (each hosting one component) to satisfy the policy.

---

**Q22. Correct: C**

SPBM continuously evaluates compliance but does not automatically move VMs. Removing the tag causes the policy check to fail, changing the compliance status to noncompliant; the administrator must manually trigger remediation (e.g., Storage vMotion) to restore compliance.

---

**Q23. Correct: A**

The Protocol Endpoint is the logical I/O proxy the array exposes to ESXi hosts; all vVol data traffic flows through the PE, which binds/unbinds vVols on demand instead of requiring a dedicated LUN per VM.

---

**Q24. Correct: A**

NFS 4.1 in vSphere supports session trunking, which allows multiple IP addresses/connections (paths) to be used for a single NFS 4.1 session, providing multipathing and increased throughput/resiliency — this requires the NFS server to also support session trunking.

---

**Q25. Correct: C**

The 'esxcli storage nmp psp roundrobin deviceconfig set' command with '--type iops --iops 1' is the correct syntax to change the Round Robin PSP's I/O operation limit per path from the default of 1000 down to 1, causing the policy to switch paths after every single I/O.

---

**Q26. Correct: C**

For RAID-1 mirroring, vSAN requires 2 x FTT + 1 hosts contributing storage. With FTT=2, that is (2 x 2) + 1 = 5 hosts minimum. The number of full data mirror copies equals FTT + 1, so FTT=2 produces 3 full mirror copies (plus witness components as needed to maintain quorum).

---

**Q27. Correct: A**

The Protocol Endpoint (PE) is the logical I/O proxy configured on the storage array and exposed to ESXi hosts; it acts as the data-path access point through which all I/O to individual vVols is routed, since vVols themselves are not directly mounted or addressed like traditional LUNs.

---

**Q28. Correct: A**

Since vSphere 7, VM Templates in Content Libraries support native version control via check-out/check-in. Checking out creates an editable VM copy; checking it back in commits the changes as a new version while retaining prior versions for rollback.

---

**Q29. Correct: C**

Cross vCenter vMotion is supported across different SSO domains, but the drag-and-drop UI workflow requires Enhanced Linked Mode. When the vCenter Servers are not linked, the API-based approach (e.g., PowerCLI Move-VM with credentials for both vCenter Servers) is required to perform the migration.

---

**Q30. Correct: D**

ESXi 8.0 introduces and supports up to virtual hardware version 20, which enables new features such as expanded vGPU and device support. VMs must be upgraded to this version to use ESXi 8.0-specific hardware capabilities.

---

**Q31. Correct: D**

The Consolidate action merges orphaned delta disks back into the base disk while the VM remains in its current running state, safely resolving the 'needs consolidation' condition without losing changes made after the failed snapshot removal.

---

**Q32. Correct: A**

For RDMs in physical compatibility mode, Storage vMotion migrates only the small mapping file that points to the LUN; the raw LUN itself and its data remain on the original physical storage device, since physical mode RDMs bypass the VMkernel's virtualization layer.

---

**Q33. Correct: C**

vSphere does not support exporting an OVF template from a VM that has VM Encryption enabled. The VM must first be decrypted (its disks and configuration data returned to unencrypted state) before the OVF export operation will succeed.

---

**Q34. Correct: B**

'Download content when needed' syncs only library item metadata (name, size, type) to the subscriber, deferring the actual file transfer until an administrator deploys or explicitly downloads the item — minimizing storage usage and WAN traffic while still allowing browsing of the catalog.

---

**Q35. Correct: C**

The 'Needs Consolidation' condition occurs when a 'Delete All' or revert operation removes the snapshot references from the VM's configuration but leaves behind orphaned delta disks (often due to an interrupted consolidation, backup software lock, or host resource contention). vCenter/ESXi detects this mismatch and flags it; running 'Consolidate' from the VM's right-click menu safely re-merges the delta disks into the base VMDK.

---

**Q36. Correct: B**

The CPU feature mask presented to a VM is established at power-on time. Enabling or changing EVC on a cluster only affects VMs at their next power-on — already-running VMs continue to expose the actual host CPU's full feature set (or their prior mask) until they are powered off and powered back on, at which point they pick up the new EVC baseline. This is a commonly-tested gotcha because vMotion alone does not re-apply the mask.

---

**Q37. Correct: B**

When Expandable Reservation is enabled on a resource pool, and the pool's own configured reservation is fully committed, the pool can dynamically borrow unused reservation capacity from its parent (up the hierarchy) as long as the parent has enough unreserved capacity — allowing the VM to power on.

---

**Q38. Correct: D**

Total cluster memory is 8 x 128 GB = 1024 GB. With a percentage-based policy reserving 25% for failover, 256 GB is set aside, leaving 1024 - 256 = 768 GB available for VM reservations.

---

**Q39. Correct: D**

'Must run on' VM/Host affinity rules are mandatory constraints enforced by both DRS and HA and can never be violated, even during an HA failover. If no host within the allowed group has sufficient capacity, the VM restart fails and the VM remains unpowered until capacity becomes available within the group.

---

**Q40. Correct: D**

vSphere Fault Tolerance supports FT-protected VMs with up to 8 vCPUs, a limit increased from the earlier 4-vCPU maximum in older vSphere releases, and this remains the supported maximum in vSphere 8.

---

**Q41. Correct: B**

vSphere uses a fixed default APD timeout of 140 seconds. Once this timeout elapses without I/O recovery, the host formally declares the device as APD, which can then trigger the cluster's configured 'Response for Datastore with APD' HA setting.

---

**Q42. Correct: B**

This is the resource pool 'sibling rivalry' behavior: shares are only meaningful relative to sibling objects sharing the same parent in the resource hierarchy. Web-01's high custom share value only influences its priority among other VMs directly inside RP-Silver. When RP-Silver as a whole competes against RP-Gold for the parent's resources, only RP-Silver's own pool-level share setting (Normal) is used in that comparison.

---

**Q43. Correct: D**

Expandable reservation allows a child resource pool to borrow unreserved reservation capacity from its parent (and ancestors) during admission control checks. If left enabled, a pool can keep reserving beyond its stated amount, consuming capacity intended for siblings. Disabling expandable reservation caps Pool-A strictly at its own 8 GHz reservation, guaranteeing Pool-B's admission control has capacity available.

---

**Q44. Correct: C**

The 'Performance degradation VMs tolerate' setting, available with the Cluster resource percentage admission control policy, lets an administrator specify the acceptable percentage of performance degradation after a failover. HA calculates whether the remaining capacity keeps degradation within this threshold and issues a cluster warning if it is exceeded, without preventing VMs from powering on.

---

**Q45. Correct: C**

vSphere Fault Tolerance protects a VM by running a live shadow instance in lockstep on a separate host, but it only supports VMs configured with up to 4 vCPUs. A 6-vCPU VM cannot be FT-protected until its vCPU count is reduced to within this supported limit, in addition to meeting other FT prerequisites such as HA being enabled on the cluster and FT-compatible CPUs across hosts.

---

**Q46. Correct: B**

High %RDY with low %USED indicates the VM's vCPUs are spending time waiting for the physical CPU scheduler due to over-provisioning/overcommitment. Right-sizing the VM (reducing vCPU count) reduces co-scheduling overhead and lets the hypervisor schedule the workload more efficiently.

---

**Q47. Correct: D**

vSphere Certificate Manager allows selective replacement of the Machine SSL certificate with a custom CA-signed certificate while VMCA continues issuing and managing ESXi host certificates independently — a supported hybrid configuration.

---

**Q48. Correct: D**

The vLCM hardware compatibility check, which integrates with a registered Hardware Support Manager, validates firmware and driver compatibility across cluster hosts against the desired image before remediation.

---

**Q49. Correct: B**

Strict Lockdown Mode stops the DCUI service entirely, removing local console management as an option; the host must be managed exclusively through vCenter Server (or via the vpxuser account).

---

**Q50. Correct: A**

vSphere permissions apply only to the object they are assigned to unless 'Propagate to children' is enabled. Without propagation, the role granted on the folder does not extend to child objects such as the VMs it contains, leaving the user with no rights on them.

---

**Q51. Correct: A**

GAVG (total guest latency) is composed of DAVG (device/array latency) plus KAVG (kernel latency). Since DAVG (40ms) accounts for nearly all of GAVG (45ms) while KAVG (5ms) is low, the bottleneck lies at the physical storage device or array, not within the ESXi kernel.

---

**Q52. Correct: D**

vLCM firmware/driver remediation via a Hardware Support Manager (e.g., Dell OMIVV, HPE OneView, Lenovo) requires an out-of-band connection to the host's BMC. If the registered BMC IP/credentials are wrong or the network path is blocked, the HSM cannot push firmware and remediation fails with exactly this communication error, isolated to that host.

---

**Q53. Correct: A**

%CSTP (co-stop) measures the percentage of time a vCPU was ready to run but was stopped so that its sibling vCPUs could catch up, a direct symptom of relaxed co-scheduling overhead on wide SMP VMs. This is the metric the exam associates with multi-vCPU scheduling skew, distinct from general ready time.

---

**Q54. Correct: D**

Hybrid mode is the documented VMCA configuration that lets you replace only the Machine SSL certificate with one issued by an external/enterprise CA while leaving all solution user certificates VMCA-signed, matching the stated requirement precisely.

---

