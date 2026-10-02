## Chapter 2: vCenter Server Deployment and Inventory Design — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | VCSA Tiny deployment size — max hosts/VMs? | 10 hosts / 100 VMs. Exam tip: smallest footprint, common for labs and small environments. |
| 2 | VCSA Small deployment size — max hosts/VMs? | 100 hosts / 1,000 VMs. |
| 3 | VCSA Medium deployment size — max hosts/VMs? | 400 hosts / 4,000 VMs. |
| 4 | VCSA Large deployment size — max hosts/VMs? | 1,000 hosts / 10,000 VMs. |
| 5 | VCSA X-Large deployment size — max hosts/VMs? | 2,000 hosts / 35,000 VMs. Exam tip: largest tier, used for massive enterprise/hyperscale environments. |
| 6 | Max number of vCenter Server instances joined via Enhanced Linked Mode? | 15 vCenter Server instances in a single SSO domain (vSphere 8 config max). Exam tip: all instances must share the same SSO domain. |
| 7 | vCenter HA architecture — node roles? | Active, Passive, Witness. Active handles all traffic; Passive is a synced standby; Witness prevents split-brain (quorum). Exam tip: 3-node design, deployed via 'Configure' workflow after basic deployment. |
| 8 | External PSC vs Embedded PSC — current status? | External PSC deprecated/removed starting vSphere 7.0. Embedded PSC (built into VCSA) is the only supported model now. Exam tip: legacy 6.x external PSC topologies must be converged before upgrading. |
| 9 | Enhanced Linked Mode (ELM) — key requirement? | All linked vCenter Server instances must join the SAME SSO domain. No external PSC required in current architecture. Exam tip: enables single pane of glass across multiple vCenters. |
| 10 | Resource Pool — what does it control? | CPU and memory allocation (shares, reservations, limits) for VMs/nested pools. Exam tip: does NOT manage storage or network resources — common trap. |
| 11 | vCenter Server file-based backup — where configured? | VAMI interface (https://<vcsa-fqdn-or-ip>:5480) or REST API. Supports FTP(S), HTTP(S), SFTP, NFS, SMB targets. Exam tip: protects config/inventory/DB, not a full VM image. |
| 12 | SSO default domain name and supported identity sources? | Default domain: vsphere.local. Identity sources: Active Directory over LDAPS, LDAP (OpenLDAP), and local OS. Exam tip: AD over LDAPS is the recommended enterprise integration method. |
