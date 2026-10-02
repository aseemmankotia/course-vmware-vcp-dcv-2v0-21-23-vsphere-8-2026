## Chapter 9: Resource Pools, Shares/Limits/Reservations, and DRS — Practice Questions

**Q1.** A cluster has two resource pools directly under the cluster root: RP-Prod (Shares: High) contains 8 VMs, and RP-Test (Shares: Normal) contains 2 VMs. During CPU contention, how are cluster CPU resources actually divided?

A) RP-Prod as a whole gets a 4:2 ratio of resources versus RP-Test, then each pool's share is divided among its own VMs, so RP-Prod VMs individually may get less per-VM than RP-Test VMs
B) Each VM in RP-Prod gets 4x the CPU of each VM in RP-Test, regardless of pool size
C) Shares are ignored because resource pools flatten all shares to the cluster root level
D) RP-Test automatically receives more resources because it has fewer VMs competing for its allocation

<details>
<summary>Answer</summary>

**Correct: A**

Shares set on a resource pool apply to the pool as a whole relative to its siblings (the pool-level 4:2 ratio), then resources allocated to the pool are further divided among the VMs inside it based on their own shares. With 8 VMs splitting the 'High' pool's allocation versus 2 VMs splitting the 'Normal' pool's allocation, each individual VM in RP-Test can end up with more effective CPU than each VM in RP-Prod — this is the classic 'resource pool sibling'/priority-pie paradox.

**Why the others are wrong:**
- Incorrect — shares do not apply directly per-VM across pool boundaries; the pool-level allocation is divided again inside each pool, so more VMs in a pool dilutes each VM's actual share.
- Incorrect — shares set on resource pools are absolutely enforced relative to sibling pools, not ignored.
- Incorrect — the ratio isn't recalculated based on VM count; it's a two-stage share calculation independent of how many VMs occupy the pool.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A VM has a memory reservation of 8GB and a memory limit of 16GB. The host is under severe memory contention and other VMs also need memory. What is guaranteed to this VM?

A) The VM is guaranteed exactly 16GB because that is the configured limit
B) The VM will receive memory purely based on its shares value since reservations only apply to CPU
C) The VM's reservation is ignored once a limit is also configured on the same object
D) The VM is guaranteed at least 8GB regardless of contention, and can consume up to but never exceed 16GB even if more is available

<details>
<summary>Answer</summary>

**Correct: D**

A reservation guarantees a minimum amount of the resource is set aside for the VM via admission control, regardless of contention. A limit caps the maximum the VM can ever consume, even when the host has spare capacity. Both settings can coexist and operate independently — 8GB minimum, 16GB maximum.

**Why the others are wrong:**
- Incorrect — a limit is a ceiling, not a guarantee; the VM is not promised the full limit amount.
- Incorrect — reservations apply equally to CPU and memory resources, not CPU only.
- Incorrect — reservations and limits are independent settings and both remain in effect simultaneously.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An administrator creates a child resource pool with a 4GHz CPU reservation under a parent resource pool that has 16GHz of reservation configured, and leaves 'Expandable Reservation' enabled (default) on the child. VMs powered on inside the child pool request a combined 6GHz reservation. What happens?

A) Admission control fails immediately because 6GHz exceeds the child pool's 4GHz reservation
B) The VMs power on but silently ignore their configured reservations
C) The child pool borrows the additional 2GHz needed from the parent's unreserved reservation capacity, allowing the VMs to power on as long as the parent has it available
D) Expandable reservation only applies to limits, not reservations, so this setting has no effect here

<details>
<summary>Answer</summary>

**Correct: C**

Expandable reservation (enabled by default on resource pools) allows a resource pool to borrow unreserved reservation capacity from its parent (and up the hierarchy) to satisfy admission control for child VMs, as long as ancestor pools have spare unreserved capacity. This lets the child pool exceed its own configured reservation when needed.

**Why the others are wrong:**
- Incorrect — admission control does not immediately fail because expandable reservation lets the pool borrow from the parent.
- Incorrect — reservations are still enforced by admission control; they are not ignored.
- Incorrect — expandable reservation specifically governs reservation borrowing behavior, not limits.

</details>

---

**Q4.** A company wants DRS to automatically perform both initial placement of new VMs and ongoing load balancing migrations without any administrator approval. Which DRS automation level should be configured?

A) Fully Automated
B) Manual
C) Partially Automated
D) Predictive Automated

<details>
<summary>Answer</summary>

**Correct: A**

Fully Automated mode has vCenter automatically perform both initial placement of powered-on VMs and ongoing vMotion migrations for load balancing without requiring the administrator to approve recommendations.

**Why the others are wrong:**
- Manual mode only provides recommendations for both placement and migration — the admin must apply them manually.
- Partially Automated automates initial placement only; migration recommendations still require manual approval.
- 'Predictive Automated' is not a valid DRS automation level — Predictive DRS is a feature that works alongside the existing automation levels, not a level itself.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A three-tier application requires that its licensing-restricted database VM must never run on any host outside a specific set of two licensed hosts in the cluster, even if this causes a temporary imbalance. Which DRS rule type correctly enforces this?

A) A 'must run on' VM-Host affinity rule (required)
B) A 'should run on' VM-Host affinity rule (preferential)
C) A VM-VM anti-affinity rule
D) A VM-VM affinity rule

<details>
<summary>Answer</summary>

**Correct: A**

'Must run on' (required) VM-Host affinity rules are hard constraints enforced by DRS and HA — the VM can never be placed or migrated to hosts outside the defined host group, satisfying strict licensing requirements even at the cost of cluster balance.

**Why the others are wrong:**
- 'Should run on' (preferred) rules are best-effort only; DRS can violate them if needed to maintain cluster health or resolve contention, which does not meet the 'never' requirement.
- VM-VM anti-affinity governs keeping two VMs apart from each other, not restricting a VM to specific hosts.
- VM-VM affinity keeps VMs together on the same host, which is unrelated to host licensing restrictions.

</details>

---

**Q6.** Which statement correctly describes the difference between shares and a reservation on a virtual machine?

A) Shares guarantee a minimum amount of resources; reservations only apply during contention
B) Shares determine relative priority only when there is resource contention; reservations guarantee a minimum amount of resources regardless of contention
C) Shares and reservations are functionally identical, differing only in configuration syntax
D) Reservations only apply to storage I/O, while shares apply to CPU and memory

<details>
<summary>Answer</summary>

**Correct: B**

Shares establish relative priority among sibling VMs/pools and only come into play when there is contention for a resource. Reservations are an absolute guarantee, checked at power-on via admission control, and are honored whether or not contention exists.

**Why the others are wrong:**
- This reverses the definitions — shares are the relative/contention-only mechanism, reservations are the guaranteed minimum.
- They serve different mechanisms entirely — one is relative priority, the other is an absolute guarantee with admission control implications.
- Reservations apply to CPU, memory, and (in some contexts) storage — this statement incorrectly limits both to the wrong scopes.

</details>

---

**Q7.** An administrator sets the DRS migration threshold to level 1 (most conservative) on a cluster. What is the effect on vMotion migration recommendations?

A) DRS migrates VMs aggressively even for small load imbalances to keep the cluster perfectly balanced at all times
B) DRS disables all automatic migrations and only allows manual vMotion
C) The migration threshold has no effect on which recommendations are generated, only on how often DRS runs
D) DRS applies only migrations that provide significant improvement, resolving only must-fix conditions like affinity rule violations or host maintenance

<details>
<summary>Answer</summary>

**Correct: D**

Migration threshold level 1 is the most conservative setting — DRS applies only priority-1 recommendations, which address mandatory conditions such as affinity/anti-affinity rule violations, host entering maintenance mode, or other must-fix conditions, rather than general load-balancing improvements.

**Why the others are wrong:**
- This describes level 5 (most aggressive), which applies even minor balancing recommendations.
- Level 1 does not disable DRS automation entirely — the automation level (Manual/Partially/Fully Automated) is a separate setting from the migration threshold.
- The threshold directly determines the priority level of recommendations that get generated/applied, not merely DRS's evaluation frequency.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** A stateless web tier of 6 identical VMs must be spread across as many different hosts as possible to maximize availability during a host failure. Which DRS rule accomplishes this?

A) VM-VM anti-affinity rule (separate VMs)
B) VM-VM affinity rule (keep VMs together)
C) VM-Host 'must run on' rule
D) A CPU reservation on each VM

<details>
<summary>Answer</summary>

**Correct: A**

A VM-VM anti-affinity rule instructs DRS to keep the specified VMs on separate hosts whenever possible, which is the standard pattern for spreading redundant/stateless tier VMs to reduce the impact of a single host failure.

**Why the others are wrong:**
- Affinity keeps VMs together on the same host, which is the opposite of the desired spread-out behavior.
- A 'must run on' VM-Host rule restricts VMs to specific hosts but doesn't by itself separate multiple VMs from each other.
- A CPU reservation only guarantees resource allocation; it has no effect on host placement or VM separation.

</details>

---

