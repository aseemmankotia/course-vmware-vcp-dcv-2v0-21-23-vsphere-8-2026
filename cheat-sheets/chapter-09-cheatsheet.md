# Chapter 9: Resource Pools, Shares/Limits/Reservations, and DRS

## Shares vs Limits vs Reservations

| Setting | Applies When | Guarantee Type | Admission Control? |
|---|---|---|---|
| **Shares** | Only during contention | Relative priority | No |
| **Reservation** | Always | Guaranteed minimum | Yes — checked at power-on |
| **Limit** | Always | Hard maximum cap | No |

- Default share ratios (CPU & memory): **High:Normal:Low = 4:2:1**
- No contention → shares have **zero** effect on allocation
- A limit is enforced even if the host has spare capacity available
- Reservation + Limit can coexist independently on the same object

## Resource Pool Hierarchy & the Sibling Trap

- Shares set on a resource pool apply **relative to sibling pools** at the same level, not globally across all VMs in the cluster
- Resources given to a pool are then **re-divided** among the VMs/child-pools inside it based on their own shares
- **Trap:** A 'High' share pool with 8 VMs may give each VM *less* than a 'Normal' share pool with only 2 VMs — because the per-VM share is diluted by pool population
- **Expandable Reservation** (default: enabled) — lets a child pool borrow unreserved reservation capacity from ancestor pools to pass admission control, even beyond its own configured reservation

## DRS Automation Levels

| Level | Initial Placement | Migration Recommendations |
|---|---|---|
| **Manual** | Recommend only | Recommend only |
| **Partially Automated** | Automatic | Recommend only (manual apply) |
| **Fully Automated** | Automatic | Automatic |

## DRS Migration Threshold (1–5, default 3)

| Level | Behavior |
|---|---|
| 1 | Conservative — only priority-1 must-fix moves (affinity violations, maintenance mode) |
| 3 | Default balance |
| 5 | Aggressive — applies even minor load-balancing moves |

## DRS Affinity / Anti-Affinity Rules

| Rule Type | Behavior |
|---|---|
| VM-VM Affinity | Keep specified VMs together on same host |
| VM-VM Anti-Affinity | Keep specified VMs apart on different hosts |
| VM-Host Affinity — **Must run on / must not run on** | Hard constraint, never violated by DRS or HA |
| VM-Host Affinity — **Should run on / should not run on** | Preferential, can be violated for cluster health |

**Precedence:** Required VM-Host rules > VM-VM affinity/anti-affinity rules.

## Predictive DRS

- Uses workload **forecast data from vRealize/Aria Operations** to proactively migrate VMs *before* a predicted demand spike occurs
- Requires DRS enabled + integration with Aria/vRealize Operations Manager
- Works alongside (does not replace) standard reactive DRS load balancing

## Exam Gotchas
- Don't assume higher pool shares = higher per-VM allocation — check sibling VM/pool count
- Limits are never bypassed by spare capacity
- 'Should' host rules ≠ guaranteed placement
- Migration threshold ≠ DRS automation level — they are independent settings
