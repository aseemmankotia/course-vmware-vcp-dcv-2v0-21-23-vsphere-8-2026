## Chapter 7: VM Creation, Templates, and Content Libraries — Practice Questions

**Q1.** An administrator needs to create a reusable master copy of a production VM but must keep the original VM running and available to users afterward. Which action should the administrator perform?

A) Convert the VM to a template
B) Take a snapshot of the VM
C) Export the VM as an OVF template and delete the source VM
D) Clone the VM to a template

<details>
<summary>Answer</summary>

**Correct: D**

Clone to Template creates a new independent template while leaving the source VM powered on and untouched.

**Why the others are wrong:**
- Convert to Template transforms the original VM into the template — it can no longer be powered on as a VM.
- A snapshot is a point-in-time disk state, not a deployable template object.
- Exporting OVF and deleting the source removes the running VM, which fails the requirement.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Which VM hardware version was introduced with ESXi 8.0 Update 2, enabling the latest virtual devices and vTPM enhancements for that release?

A) Hardware version 17
B) Hardware version 19
C) Hardware version 21
D) Hardware version 20

<details>
<summary>Answer</summary>

**Correct: C**

Hardware version 21 was introduced with ESXi 8.0 U2.

**Why the others are wrong:**
- Hardware version 17 corresponds to ESXi 7.0 GA.
- Hardware version 19 corresponds to ESXi 7.0 U2.
- Hardware version 20 corresponds to ESXi 8.0 GA, not the U2 release.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A company operates vCenter Server instances at two sites and wants templates published once and automatically kept in sync at the remote site without manual export/import for every update. Which solution BEST meets this requirement?

A) Manually export each template as OVF and re-import it at the remote site after every change
B) Publish a local Content Library and create a subscribed library at the remote vCenter with automatic sync
C) Use Cross vCenter vMotion to move templates between sites
D) Create a Customization Specification and copy it to the remote vCenter

<details>
<summary>Answer</summary>

**Correct: B**

Publishing a local Content Library and subscribing to it from the remote vCenter automatically syncs library content, eliminating manual export/import.

**Why the others are wrong:**
- Manual OVF export/import is exactly the repetitive manual process the company wants to avoid.
- vMotion migrates running VMs, not template libraries, and doesn't work this way across independent Content Libraries.
- Customization Specifications personalize guest OS settings, not template distribution.

</details>

---

**Q4.** An administrator wants a subscribed Content Library to minimize storage and bandwidth usage until a template is actually needed for deployment. Which sync configuration should be used?

A) Immediate sync of all library content
B) Disable syncing entirely on the subscribed library
C) On-demand sync (download content only when needed)
D) Convert the subscribed library to a local library

<details>
<summary>Answer</summary>

**Correct: C**

On-demand sync downloads only metadata initially and pulls item content only when a VM is deployed from it, saving storage and bandwidth.

**Why the others are wrong:**
- Immediate sync downloads all content right away, consuming more storage/bandwidth than required.
- Disabling sync would prevent the subscribed library from receiving any updates at all.
- Converting to a local library removes the subscription relationship and breaks automated updates from the source.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** Which file format packages the OVF descriptor, virtual disks, and manifest into a single portable archive file for VM template distribution?

A) OVA
B) OVF
C) VMTX
D) VMDK

<details>
<summary>Answer</summary>

**Correct: A**

OVA (Open Virtual Appliance) bundles all OVF-related files into one tar archive.

**Why the others are wrong:**
- OVF is the descriptor format that normally exists as multiple separate files (.ovf, .vmdk, .mf).
- VMTX is the template configuration file used internally by vCenter, not an export format.
- VMDK is only the virtual disk file, not a complete package.

</details>

---

**Q6.** An administrator needs to deploy 50 Windows Server VMs from a single template, each requiring a unique hostname, SID, and IP address automatically during deployment. Which feature should be applied?

A) OVF properties defined in the template
B) Content Library subscription sync
C) A Customization Specification
D) Convert VM to Template

<details>
<summary>Answer</summary>

**Correct: C**

Customization Specifications automate guest OS personalization (hostname, SID via Sysprep, IP configuration) applied during deployment from a template.

**Why the others are wrong:**
- OVF properties are typically used for vApp parameterization, not standard Windows Sysprep-style personalization.
- Content Library sync only distributes library content; it does not personalize guest OS settings.
- Convert VM to Template only creates the template object and does not personalize deployed clones.

</details>

---

**Q7.** A Horizon administrator needs to provision hundreds of desktop VMs quickly while minimizing storage consumption, with each desktop referencing a shared base disk and writing changes to a per-VM delta disk. Which technology accomplishes this?

A) Linked clones
B) Full clones
C) Content Library OVA deployment
D) Cross vCenter vMotion

<details>
<summary>Answer</summary>

**Correct: A**

Linked clones share a parent/replica base disk and write changes to per-VM delta disks, enabling fast provisioning and reduced storage use.

**Why the others are wrong:**
- Full clones create complete independent disk copies, using significantly more storage and provisioning time.
- OVA deployment creates independent full VMs from an archive, not space-efficient linked clones.
- vMotion migrates running VMs and does not perform desktop provisioning.

</details>

---

**Q8.** An administrator exports a VM configured with hardware version 20 as an OVF template and attempts to deploy it into a vCenter Server whose hosts run only ESXi 6.7 (maximum supported hardware version 14). What is the MOST likely outcome?

A) The import automatically downgrades the VM to hardware version 14 with no warning
B) The deployment wizard blocks or warns that the hardware version is unsupported on the target hosts
C) The VM deploys normally but ignores hardware version entirely
D) The OVF file becomes corrupted during export due to version mismatch

<details>
<summary>Answer</summary>

**Correct: B**

vCenter checks hardware version compatibility against the target host's maximum supported version and blocks or warns when incompatible.

**Why the others are wrong:**
- Hardware version downgrade is not automatic during OVF import; compatibility must be manually addressed.
- Hardware version directly determines available virtual devices/features and cannot simply be ignored.
- Export itself completes fine; the incompatibility surfaces at import/deploy time, not during export.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

