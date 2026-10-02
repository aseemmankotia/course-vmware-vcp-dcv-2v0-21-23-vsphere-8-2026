## Chapter 7: VM Creation, Templates, and Content Libraries — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | ESXi 8.0 GA maps to which VM hardware version? | Hardware version 20. Exam tip: ESXi 8.0 U2 introduced hardware version 21. |
| 2 | ESXi 7.0 U2 maps to which VM hardware version? | Hardware version 19 (base ESXi 7.0 is hardware version 17). |
| 3 | ESXi 6.7 maps to which VM hardware version? | Hardware version 14. |
| 4 | OVF vs OVA — structural difference? | OVF = separate files (.ovf descriptor, .vmdk disks, .mf manifest) kept in one folder. OVA = single tar archive bundling all of them into one portable file. |
| 5 | Convert VM to Template vs Clone VM to Template? | Convert: original VM becomes the template and can no longer run. Clone: original VM stays running; a separate independent template is created. Exam tip: use Clone when source must stay in production. |
| 6 | Local Content Library vs Subscribed Content Library? | Local = authoritative source, created/managed in current vCenter, can be published. Subscribed = points to a published library's URL, pulls a synced (read-only) copy of content. |
| 7 | Two sync modes for a subscribed Content Library? | Immediate sync (downloads all content right away) vs On-demand sync (metadata only, content pulled when deployed). On-demand saves storage/bandwidth. |
| 8 | Required power state to Convert to Template or Export OVF Template? | VM must be powered off. Exam trap: option is greyed out on a powered-on VM. |
| 9 | What does a Customization Specification do? | Automates guest OS personalization (hostname/SID, IP, domain join) during deployment/cloning from a template. Windows uses Sysprep under the hood. |
| 10 | Linked Clone vs Full Clone (VDI/Horizon)? | Linked clone: shares parent base/replica disk, writes to per-VM delta disk — fast, storage-efficient, some I/O dependency on parent. Full clone: complete independent disk copy — slower to provision, more storage, isolated performance. |
| 11 | How to distribute a template automatically to multiple remote vCenter Servers? | Publish a local Content Library, then create subscribed libraries at each remote vCenter to auto-sync content. |
| 12 | Can a VM template be powered on directly? | No. A template is not runnable; you must deploy a new VM from it first. Exam trap: templates never appear as powered-on objects. |
