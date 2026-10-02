## Chapter 3: Standard and Distributed Virtual Switches — Practice Questions

**Q1.** A VM runs a nested hypervisor and must send/receive traffic tagged for VLANs 10, 20, and 30 through a single vNIC connected to a distributed port group. The physical switch port is configured as an 802.1Q trunk. Which VLAN tagging configuration on the port group meets this requirement?

A) VLAN ID set to 4095 (Virtual Guest Tagging)
B) VLAN ID set to 0 (External Switch Tagging)
C) VLAN ID set to 20 (Virtual Switch Tagging)
D) VLAN Trunking disabled with native VLAN 1

<details>
<summary>Answer</summary>

**Correct: A**

VGT (VLAN ID 4095) passes all tagged frames untouched to the guest OS, which must run its own 802.1Q driver to process multiple VLANs over one vNIC — required for nested hypervisors or VMs that need multi-VLAN awareness.

**Why the others are wrong:**
- EST (VLAN 0) means the switch strips tags before frames reach the vSwitch — no VLAN tagging is visible to the VM at all.
- VST assigns exactly one VLAN ID per port group; the VM would only see VLAN 20 traffic, not 10 or 30.
- Disabling trunking with native VLAN 1 is not a real vSphere VLAN mode and would only pass untagged traffic.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An architect must migrate 200 production VMs from a vSphere Standard Switch to a Distributed Switch across a 12-host cluster with zero application downtime. Which approach BEST achieves this?

A) Power off each VM, delete its vSS network adapter, and manually assign it to the vDS port group
B) Use the 'Migrate VMs to Another Network' wizard to move VM network adapters from vSS port groups to matching vDS port groups while VMs remain powered on
C) Delete the vSS on each host first, then create the vDS and reconnect VMs afterward
D) Recreate all VMs on new hosts already connected to the vDS

<details>
<summary>Answer</summary>

**Correct: B**

The Migrate VMs to Another Network wizard (or Add and Manage Hosts workflow) reassigns the vNIC of running VMs to an equivalent vDS port group with no packet loss beyond normal link renegotiation — the standard supported zero-downtime migration path.

**Why the others are wrong:**
- Powering off VMs causes application downtime, violating the requirement.
- Deleting the vSS first removes connectivity for any VM still attached to it before migration.
- Recreating VMs is unnecessary, extremely disruptive, and not a supported migration method.

</details>

---

**Q3.** A company wants to guarantee that vMotion traffic never starves vSAN traffic during periods of network congestion, using shares, reservations, and limits enforced by the hypervisor itself. Which solution meets this requirement?

A) vSphere Standard Switch with traffic shaping enabled on the vMotion port group
B) vSphere Distributed Switch with Network I/O Control (NIOC) configured on system traffic
C) vSphere Standard Switch with explicit failover order on two uplinks
D) vSphere Distributed Switch with Private VLANs isolating vMotion traffic

<details>
<summary>Answer</summary>

**Correct: B**

NIOC is a vDS-only feature that lets you set shares, reservations, and limits per system traffic type (vMotion, vSAN, Management, etc.) to guarantee bandwidth allocation dynamically during contention.

**Why the others are wrong:**
- vSS traffic shaping only limits outbound traffic (average bandwidth, burst, peak) — it cannot guarantee minimum bandwidth via reservations.
- Explicit failover order controls which uplink is active, not bandwidth allocation between traffic types.
- PVLANs provide Layer 2 isolation for security/micro-segmentation, not bandwidth guarantees.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Within a Private VLAN configuration on a distributed port group, a VM is assigned to an Isolated secondary VLAN. With which other ports can this VM communicate at Layer 2?

A) Any port in the same Community secondary VLAN
B) Only ports configured as Promiscuous on the Primary VLAN
C) Any port in the same Primary VLAN regardless of secondary type
D) No other ports — isolated VMs are always fully blocked

<details>
<summary>Answer</summary>

**Correct: B**

Isolated PVLAN ports can only send/receive traffic to/from Promiscuous ports (typically a router or gateway); they cannot talk to each other or to Community ports.

**Why the others are wrong:**
- Community ports can talk to each other and to Promiscuous ports, but an Isolated port cannot reach Community ports.
- Sharing the same Primary VLAN does not grant communication — secondary VLAN type governs Layer 2 reachability.
- Isolated ports can still reach the Promiscuous port, so they are not fully blocked.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** An administrator configures a distributed port group with VLAN ID 0 while the upstream physical switch port is set as an untagged access port. Which VLAN tagging mode is in effect?

A) Virtual Guest Tagging (VGT)
B) Virtual Switch Tagging (VST)
C) External Switch Tagging (EST)
D) Private VLAN tagging

<details>
<summary>Answer</summary>

**Correct: C**

VLAN ID 0 disables tagging at the vSwitch/port group level, meaning any VLAN assignment happens entirely on the physical access switch — this is EST.

**Why the others are wrong:**
- VGT uses VLAN ID 4095, not 0, and requires a trunk port upstream plus guest-OS tagging.
- VST requires a specific non-zero, non-4095 VLAN ID assigned at the port group level.
- Private VLAN tagging is a separate secondary-VLAN mechanism, not indicated by VLAN ID 0 alone.

</details>

---

**Q6.** A cluster contains a mix of ESXi 7.0 U3 and ESXi 8.0 hosts. The design requires the newest Distributed Switch features available while still allowing the ESXi 7.0 U3 hosts to join. Which vDS version should be selected?

A) vDS 8.0.0
B) vDS 6.6.0
C) vDS 7.0.3
D) vDS 8.0.2

<details>
<summary>Answer</summary>

**Correct: C**

vDS 7.0.3 is the minimum vDS version compatible with ESXi 7.0 U3 hosts while still being current for that host, allowing mixed 7.0 U3 and 8.0 hosts to join the same switch.

**Why the others are wrong:**
- vDS 8.0.0 and 8.0.2 require a minimum host version of ESXi 8.0 — 7.0 U3 hosts cannot join, and would be greyed out/incompatible in the wizard.
- vDS 6.6.0 works with older hosts but omits newer feature sets available in 7.x, so it is not the best fit versus 7.0.3.
- null

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A design requires that active/active load balancing across two 10GbE uplinks on a vDS dynamically shift VM traffic based on real-time physical NIC utilization, without requiring any physical switch-side EtherChannel/LAG configuration. Which vDS teaming and failover policy should be configured?

A) Route based on IP hash
B) Route based on originating virtual port
C) Use explicit failover order
D) Route based on physical NIC load (Load Based Teaming)

<details>
<summary>Answer</summary>

**Correct: D**

Load Based Teaming (LBT) is a vDS-only teaming policy that monitors uplink utilization every 30 seconds and rebalances VM traffic dynamically across uplinks with no physical switch configuration required.

**Why the others are wrong:**
- Route based on IP hash requires static EtherChannel/LAG configuration on the physical switch — it is not dynamic based on load.
- Route based on originating virtual port statically pins a VM to one uplink at connect time; it does not rebalance based on current load.
- Explicit failover order is active/standby, not active/active load balancing.

</details>

---

**Q8.** Which statement correctly differentiates a vSphere Standard Switch (vSS) from a vSphere Distributed Switch (vDS)?

A) vSS is configured and maintained independently on each host, while vDS provides a single centrally managed switch construct spanning multiple hosts
B) vSS configuration is centrally managed from vCenter and applies cluster-wide, while vDS must be configured on each host individually
C) Both vSS and vDS require vCenter Server to exist and function
D) vSS supports Network I/O Control while vDS does not

<details>
<summary>Answer</summary>

**Correct: A**

vSS is a per-host construct with its own independent configuration on every ESXi host; vDS is created and managed centrally through vCenter and presents a single logical switch spanning all member hosts.

**Why the others are wrong:**
- This reverses the actual architecture — vDS, not vSS, is centrally managed via vCenter.
- vSS does not require vCenter at all and can be fully configured via the host client even without vCenter present.
- NIOC is exclusively a vDS feature; vSS does not support it.

</details>

---

