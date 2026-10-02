## Chapter 4: VMkernel Adapters, NIC Teaming, and Network I/O Control — Practice Questions

**Q1.** A vSphere admin configures a standard switch's NIC teaming policy to 'Route based on IP hash' to increase throughput for a group of VMs. After applying the change, several VMs on that switch lose network connectivity intermittently. What is the MOST likely cause?

A) The VMkernel adapter for vMotion is using the same uplink
B) NIOC shares for virtual machine traffic are set too low
C) The vSwitch MTU does not match the VM's guest OS MTU
D) The physical switch ports are not configured as a static EtherChannel (link aggregation) group

<details>
<summary>Answer</summary>

**Correct: D**

IP hash load balancing requires the physical switch ports to be configured in a static EtherChannel (802.3ad static, not LACP) so both sides agree on how to distribute frames across links; mismatched configuration causes flapping/connectivity loss.

**Why the others are wrong:**
- vMotion adapter placement doesn't cause VM traffic connectivity loss from IP hash misconfiguration
- NIOC shares only affect bandwidth contention, not connectivity drops
- MTU mismatch causes fragmentation/performance issues, not the intermittent loss pattern typical of IP hash misconfiguration

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An administrator needs to reduce vMotion migration time for hosts with four 10GbE uplinks dedicated to vMotion traffic. Which configuration BEST achieves this?

A) Increase the NIOC shares value for the vMotion traffic type to 100
B) Configure multiple VMkernel adapters for vMotion, each assigned a different active uplink with the others as standby
C) Configure a single VMkernel adapter for vMotion and set jumbo frames only
D) Enable Fault Tolerance logging on the same VMkernel adapter used for vMotion

<details>
<summary>Answer</summary>

**Correct: B**

Multi-NIC vMotion requires creating multiple VMkernel adapters, each with a different uplink set as active and the remaining uplinks set to standby (opposite order per adapter), allowing vMotion to use all available uplinks simultaneously.

**Why the others are wrong:**
- NIOC shares only govern contention when bandwidth is oversubscribed; they don't parallelize vMotion across NICs
- A single VMkernel adapter can only utilize one active uplink at a time regardless of jumbo frames
- FT logging is a separate traffic type and mixing it doesn't increase vMotion throughput

</details>

---

**Q3.** On a distributed switch with Network I/O Control enabled, an admin attempts to set reservations for vMotion (10 Gbps), vSAN (10 Gbps), and Management (2 Gbps) traffic on hosts where the physical adapter with the least capacity is a 10GbE NIC. What happens when the admin tries to save this configuration?

A) The configuration saves successfully because reservations apply per-VM, not per-adapter
B) The configuration is rejected because total reservations exceed 75% of the capacity of the adapter with the least bandwidth
C) The configuration saves but vSAN traffic is automatically throttled to 25%
D) The configuration saves only if Network I/O Control version 2 is used instead of version 3

<details>
<summary>Answer</summary>

**Correct: B**

NIOC enforces an admission-control rule: the sum of all reservations across traffic types cannot exceed 75% of the bandwidth of the physical adapter with the least capacity connected to the switch (7.5 Gbps of 10 Gbps here), and 22 Gbps far exceeds that.

**Why the others are wrong:**
- NIOC reservations apply at the traffic-type (system traffic) level on the vDS, not solely per-VM
- Traffic isn't silently throttled — the reservation configuration itself is rejected/blocked
- The 75% admission control rule applies to NIOC version 3, which is the version required for reservations at all

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Which VMkernel adapter service must be explicitly enabled to allow a host to participate in a vSAN cluster and exchange vSAN cluster traffic?

A) Provisioning
B) Management
C) vSAN
D) NFC (Network File Copy)

<details>
<summary>Answer</summary>

**Correct: C**

The vSAN service must be enabled on a VMkernel adapter for a host to communicate vSAN metadata and data traffic within the cluster; it is a distinct required checkbox in VMkernel adapter properties.

**Why the others are wrong:**
- Provisioning covers cold migration, cloning, and snapshot operations, not vSAN cluster communication
- Management handles host-to-vCenter and ESXCLI/API traffic, not vSAN data traffic
- NFC handles file copy operations like cold migration to datastores without vMotion, not vSAN cluster membership

</details>

---

**Q5.** A company performs frequent cold migrations and template deployments across hosts and wants this traffic isolated from vMotion traffic using its own routing table. Which feature should be configured?

A) Create a VMkernel adapter with the Provisioning TCP/IP stack
B) Enable the Fault Tolerance logging service on the vMotion VMkernel adapter
C) Increase the NIOC limit for the vMotion traffic type
D) Configure the Management VMkernel adapter with a static route

<details>
<summary>Answer</summary>

**Correct: A**

The Provisioning TCP/IP stack is a dedicated custom stack (separate from the default and vMotion stacks) used for NFC-based operations like cold migration, cloning, and snapshot/template operations, with its own routing table and gateway.

**Why the others are wrong:**
- FT logging is unrelated to cold migration/provisioning traffic isolation
- NIOC limits control bandwidth caps, not traffic isolation via separate routing
- A static route on the Management stack does not separate provisioning traffic into its own stack

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** An admin wants to enable jumbo frames to improve vSAN and vMotion performance across a cluster. Which set of components must ALL be configured with an MTU of 9000 for jumbo frames to work end-to-end?

A) Only the VMkernel adapter's MTU needs to be changed
B) The virtual switch (or portgroup), the VMkernel adapter, and the physical switch ports/uplinks
C) Only the physical switch needs the MTU changed; ESXi auto-negotiates
D) The guest OS network adapter MTU only, since VMkernel traffic ignores MTU settings

<details>
<summary>Answer</summary>

**Correct: B**

End-to-end jumbo frame support requires MTU 9000 configured consistently on the vSwitch/vDS (or portgroup for vDS), the VMkernel adapter itself, and every physical switch port/uplink in the path — a mismatch anywhere causes fragmentation or dropped packets.

**Why the others are wrong:**
- Changing only the VMkernel adapter without the switch layers causes MTU mismatch and packet drops
- ESXi does not auto-negotiate jumbo frames; MTU must be explicitly set at every layer
- This scenario concerns VMkernel (vSAN/vMotion) traffic, not guest OS VM traffic

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** On a distributed switch, an admin configures the 'Route based on physical NIC load' teaming policy. What is the exam-tested behavior of this Load Based Teaming (LBT) algorithm?

A) It rebalances traffic when an uplink's utilization exceeds 75% over a 30-second interval, and it is only available on a distributed switch
B) It moves traffic to a different uplink whenever any packet loss is detected
C) It requires static EtherChannel configuration on the physical switch like IP hash
D) It is the default teaming policy for both standard and distributed switches

<details>
<summary>Answer</summary>

**Correct: A**

LBT (Route based on physical NIC load) is exclusive to vSphere Distributed Switches and rebalances flows to other active uplinks when mean utilization exceeds 75% over a 30-second sampling period.

**Why the others are wrong:**
- LBT reacts to sustained utilization thresholds, not individual packet loss events
- LBT does not require special physical switch link aggregation configuration, unlike IP hash
- The default policy on both standard and distributed switches is Route based on originating virtual port ID, not LBT

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Why does vSphere provide a dedicated vMotion TCP/IP stack instead of using the default stack for vMotion traffic?

A) It allows vMotion traffic to bypass Network I/O Control entirely
B) It is required to enable Multi-NIC vMotion; Multi-NIC vMotion cannot function on the default stack under any configuration
C) It automatically encrypts vMotion traffic between hosts
D) It provides an isolated routing table and default gateway so vMotion traffic can be routed across networks without affecting the default management routing table

<details>
<summary>Answer</summary>

**Correct: D**

The vMotion TCP/IP stack maintains its own routing table, default gateway, and DNS configuration separate from the default stack, allowing vMotion traffic to be routed across L3 networks without altering the host's default management routes.

**Why the others are wrong:**
- NIOC still applies to vMotion traffic regardless of which TCP/IP stack is used
- Multi-NIC vMotion can technically use the default stack, though the vMotion stack is recommended for routed configurations
- Encryption of vMotion is a separate feature (encrypted vMotion) configured per-VM, unrelated to the TCP/IP stack choice

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

