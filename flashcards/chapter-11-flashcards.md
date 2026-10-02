## Chapter 11: Security, Roles, Lifecycle Management, and Performance Troubleshooting — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | When a permission is defined directly on a VM but a different one is inherited from its parent folder, which wins? | The permission defined directly on the object always overrides the inherited one, regardless of role scope. |
| 2 | Default state of 'Propagate to children' when assigning a vSphere permission via the UI? | Checked (enabled) by default — uncheck it to restrict the assignment to a single object only. |
| 3 | Which three vCenter roles are system roles that cannot be deleted or edited? | Administrator, Read-Only, and No Access. Sample roles (e.g., Virtual Machine Power User) are templates meant to be cloned, not edited directly. |
| 4 | Can a cluster be managed by both vLCM images and legacy baselines simultaneously? | No. A cluster is exclusively baseline-managed (legacy) or image-managed (vLCM desired state) — never both at once. |
| 5 | What makes up a vLCM 'desired image'? | ESXi base image + vendor add-on + optional firmware/driver add-on (via Hardware Support Manager) + components. |
| 6 | esxtop %RDY red-flag threshold per vCPU? | Sustained %RDY above roughly 5-10% per vCPU indicates CPU scheduling contention. Measured per vCPU, not per VM total. |
| 7 | What does esxtop's %CSTP metric measure and what fixes a high value? | Co-stop: time an SMP VM's vCPUs wait to be co-scheduled together. Fix by reducing the VM's vCPU count to match real workload parallelism. |
| 8 | esxtop disk latency: DAVG vs KAVG vs GAVG? | DAVG = physical device latency; KAVG = VMkernel queue latency; GAVG = guest-observed latency (DAVG + KAVG). High KAVG with low DAVG = queue depth problem in ESXi, not the array. |
| 9 | Default vCenter certificate management mode after a fresh install? | VMCA mode — VMCA acts as root CA and auto-issues/renews all solution-user and machine certificates. |
| 10 | How can an org use its own root CA while keeping VMCA's automatic certificate issuance? | Configure VMCA as a subordinate (intermediate) CA under the corporate root CA — VMCA still auto-issues certs but they chain to the enterprise root. |
| 11 | Command to generate an ESXi support bundle with an esxtop performance snapshot? | vm-support -p -d <duration> -i <interval>. Plain 'vm-support' collects logs/config but no live perf capture. |
| 12 | Key log files to check first for vCenter/host connectivity issues? | vpxd.log (vCenter service), vpxa.log (host agent-to-vCenter link), hostd.log (host management agent), vmkernel.log (ESXi kernel/storage/network events). |
