## Chapter 6: vSAN and Storage Policy-Based Management (SPBM) — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | vSAN standard cluster minimum host count? | 3 hosts. Two-node topology uses 2 data hosts + 1 witness. Exam tip: don't confuse 'minimum hosts' with 'minimum for RAID-5/6'. |
| 2 | Minimum hosts for RAID-5 erasure coding (FTT=1)? | 4 hosts (3 data + 1 parity, 3+1 scheme). RAID-5 only supports FTT=1. |
| 3 | Minimum hosts for RAID-6 erasure coding (FTT=2)? | 6 hosts (4 data + 2 parity, 4+2 scheme). RAID-6 only supports FTT=2. |
| 4 | RAID-1 mirroring capacity overhead at FTT=1 vs FTT=2? | FTT=1 = 2x storage (2 copies, 3 hosts min). FTT=2 = 3x storage (3 copies, 5 hosts min). FTT=3 = 4x storage, 7 hosts min. |
| 5 | RAID-5 vs RAID-6 vs RAID-1: capacity overhead comparison for equivalent FTT=2? | RAID-6 (1.5x) is far more space-efficient than RAID-1 (3x) for the same FTT=2 protection level, at the cost of more write amplification/CPU. |
| 6 | vSAN OSA cache tier device type? | Always SSD/flash, even in hybrid disk groups. Hybrid: cache = read cache + write buffer. All-flash: cache = write buffer only. |
| 7 | vSAN ESA vs OSA — key architectural difference? | ESA: no disk groups, single per-host storage pool across all-flash NVMe, log-structured filesystem, native efficient erasure coding. OSA: disk groups with separate cache+capacity tiers. |
| 8 | vVols core components? | Storage Container (capacity pool on array), Protocol Endpoint/PE (I/O access point), VASA Provider (control plane/storage awareness). VM objects: Config, Data, Swap, optional Memory vVol. |
| 9 | vVols vs traditional VMFS/NFS — data services granularity? | vVols apply array-native snapshots/replication/QoS per-VM (per VMDK). VMFS/NFS apply them per-datastore/LUN, affecting all VMs sharing it. |
| 10 | vSAN stretched cluster RTT requirement between the two data sites? | ≤5ms RTT required between active/active data sites for synchronous writes to succeed with acceptable performance. |
| 11 | Default vSAN Object Repair Timer value? | 60 minutes. Controls how long vSAN waits before starting a full resync of an absent component after a transient failure (e.g., host reboot). |
| 12 | vSAN stretched cluster fault domain design? | Two fault domains (Preferred and Secondary site), each hosting data components, plus a witness host/appliance at a third site holding only witness components (no VM data). |
