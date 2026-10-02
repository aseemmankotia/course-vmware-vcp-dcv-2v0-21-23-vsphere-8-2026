## Chapter 3: Standard and Distributed Virtual Switches — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | vSS vs vDS: which is configured per-host and which is centrally managed? | vSS = configured independently on each ESXi host. vDS = single logical switch centrally managed from vCenter, spanning multiple hosts. Exam tip: vDS requires vCenter to exist/be managed; vSS does not. |
| 2 | VLAN ID value used for External Switch Tagging (EST)? | VLAN ID = 0. Tagging happens entirely on the physical switch; the ESXi vSwitch/port group never sees a tag. Exam tip: physical switch port is an access port. |
| 3 | VLAN ID value used for Virtual Guest Tagging (VGT)? | VLAN ID = 4095. All tagged frames pass through untouched; the guest OS must run its own 802.1Q driver. Physical switch port must be a trunk. |
| 4 | Virtual Switch Tagging (VST) — what VLAN ID range and who tags/untags frames? | VLAN ID = 1–4094 (a specific single VLAN). ESXi vSwitch/port group adds/strips the tag; physical switch port is a trunk. This is the most common configuration. |
| 5 | Which vSwitch type supports Network I/O Control (NIOC)? | Only vDS. NIOC provides shares, reservations, and limits per system traffic type (vMotion, vSAN, Management, etc.). Not available on vSS at all. |
| 6 | PVLAN secondary type: Isolated — who can it communicate with? | Only with Promiscuous ports. Cannot talk to other Isolated ports or Community ports on the same primary VLAN. |
| 7 | PVLAN secondary type: Community — who can it communicate with? | Other ports in the same Community secondary VLAN, plus Promiscuous ports. Cannot reach Isolated ports. |
| 8 | PVLAN Promiscuous port purpose? | Can communicate with all ports on the primary VLAN (Isolated, Community, and other Promiscuous ports) — typically used for the gateway/router uplink. |
| 9 | vDS teaming policy for dynamic active/active load balancing without physical switch LAG config? | Route based on physical NIC load (Load Based Teaming / LBT). Rechecks uplink utilization every 30 seconds. vDS-only feature — not available on vSS. |
| 10 | Minimum ESXi version required to join a vDS version 8.0.0? | ESXi 8.0. Higher vDS versions require a minimum matching (or newer) ESXi host version — older hosts cannot join a newer vDS version. |
| 11 | Route based on IP hash — what physical switch requirement does it have? | Requires static EtherChannel or LACP (LAG) configured on the physical switch side. Mismatched config causes network outages — common exam trap. |
| 12 | Zero-downtime method to move VM vNICs from vSS port groups to vDS port groups? | Use the 'Migrate VMs to Another Network' wizard (or Add and Manage Hosts > Migrate VM networking) while VMs stay powered on. No VM reboot or power-off required. |
