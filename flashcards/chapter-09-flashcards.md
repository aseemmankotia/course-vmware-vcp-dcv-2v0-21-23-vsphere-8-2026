## Chapter 9: Resource Pools, Shares/Limits/Reservations, and DRS — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Default share ratio for High:Normal:Low on CPU and memory? | 4:2:1. Exam tip: shares only matter during contention — no contention means shares have zero effect on allocation. |
| 2 | Reservation vs Limit — which one is checked by admission control at VM power-on? | Reservation. A limit is never checked by admission control since it only restricts maximum usage, not guaranteed minimums. |
| 3 | What is the 'resource pool sibling' / priority-pie paradox? | Shares apply at the pool level relative to sibling pools, then are re-divided among VMs inside each pool. A pool with fewer VMs can give each VM more effective resources than a 'higher priority' pool with many VMs. |
| 4 | What does 'Expandable Reservation' allow a child resource pool to do? | Borrow unreserved reservation capacity from its parent pool (and ancestors) to satisfy admission control, even if it exceeds the child's own configured reservation. Enabled by default. |
| 5 | List the three DRS automation levels. | Manual (recommendations only, both placement and migration), Partially Automated (auto initial placement, manual migration approval), Fully Automated (both automatic). |
| 6 | DRS migration threshold range and default value? | 1 (conservative, only must-fix priority-1 recommendations) to 5 (aggressive, applies even minor balancing moves). Default is level 3. |
| 7 | VM-Host affinity: 'must run on' vs 'should run on' — key exam difference? | 'Must run on/must not run on' = hard constraint enforced by DRS and HA, never violated. 'Should run on/should not run on' = preferential, can be violated if needed for cluster health. |
| 8 | What is Predictive DRS and what does it require? | Predictive DRS proactively migrates VMs ahead of a forecasted resource demand spike, using workload forecast data from vRealize/Aria Operations integrated with the cluster (in addition to standard DRS). |
| 9 | VM-VM anti-affinity rule — primary exam use case? | Spread redundant/identical VMs (e.g., web tier nodes) across separate hosts to maximize availability during a host failure. |
| 10 | Does a Limit setting ever get overridden if the host has spare capacity? | No — a limit is a hard cap that is enforced regardless of available host resources. Common exam trap: assuming spare capacity lets the VM exceed its limit. |
| 11 | If no contention exists on a host, what effect do Shares have? | None — Shares only influence resource allocation during contention. With ample resources, all VMs get what they request up to their limit. |
| 12 | Which DRS rule type has priority when a VM-Host 'must run on' rule conflicts with a VM-VM affinity rule? | Required VM-Host affinity/anti-affinity rules always take precedence over VM-VM affinity/anti-affinity rules — DRS will not violate a 'must' host rule to satisfy a VM-VM rule. |
