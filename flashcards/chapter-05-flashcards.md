## Chapter 5: Datastores: VMFS, NFS, Storage Adapters, and Multipathing — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | VMFS6 fixed block size? | 1MB (single block size for all VMFS6 volumes, unlike VMFS5's multiple block size options). Exam tip: VMFS5 used 1MB blocks by default too, but earlier upgraded VMFS3 volumes could have larger blocks — VMFS6 standardizes to 1MB. |
| 2 | VMFS6 automatic space reclamation (UNMAP) default behavior? | Enabled by default, runs asynchronously in the background, default priority is Low. Can be set to None or Low via esxcli/UI. Exam tip: VMFS5 requires manual UNMAP via esxcli; VMFS6 automates it. |
| 3 | VMFS6 disk sector format support? | Supports both 512e (512-byte emulation) and 4Kn (4K native) disks. VMFS5 supports 512n and 512e only, not 4Kn. Exam tip: 4Kn support is a key VMFS6-only differentiator. |
| 4 | NFS 3 vs NFS 4.1: which supports Kerberos authentication? | Only NFS 4.1. Modes: krb5 (authentication only) and krb5i (authentication + integrity). NFS 3 only supports AUTH_SYS (host trust). |
| 5 | NFS 4.1 multipathing mechanism? | Uses session trunking (native multipathing) over multiple physical NICs/paths. NFS 3 has no native multipathing — relies on network-layer teaming/failover instead. |
| 6 | Three types of iSCSI adapters? | 1) Software iSCSI (VMkernel handles all processing), 2) Dependent hardware iSCSI (uses ESXi network config, partial offload), 3) Independent hardware iSCSI (fully self-contained, full offload of network + iSCSI processing). |
| 7 | NVMe over Fabrics transport options supported by ESXi? | NVMe over FC, NVMe over RDMA (RoCE v2), NVMe over TCP. Exam tip: know which transport requires which physical adapter (RDMA-capable NIC for RoCE, standard NIC for NVMe/TCP). |
| 8 | iSCSI dynamic vs static target discovery? | Dynamic (SendTargets): host queries array/target, returns all available targets automatically. Static: admin manually enters target IQN + IP, no query performed. |
| 9 | CHAP one-way vs mutual? | One-way (unidirectional): only the initiator authenticates to the target. Mutual (bidirectional): both initiator and target authenticate each other. |
| 10 | PSP Fixed vs MRU failback behavior? | Fixed: uses a preferred path, automatically fails back to it once restored. MRU: no preferred path concept, continues using the last active path even after original path recovers. |
| 11 | Round Robin PSP default I/O switching threshold? | 1000 I/O operations per path (or 10MB) before switching to next active path. Exam tip: Round Robin is the VMware-recommended default PSP for most modern arrays. |
| 12 | RDM physical vs virtual compatibility mode? | Physical (pRDM): passes nearly all SCSI commands directly to LUN, no snapshots, required for cross-host WSFC/SCSI-3 reservations. Virtual (vRDM): LUN attributes virtualized, supports snapshots/cloning, behaves more like a VMDK. |
