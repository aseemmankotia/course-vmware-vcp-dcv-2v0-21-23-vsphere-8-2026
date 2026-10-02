# Chapter 9 Lab: Resource Pools, Shares/Limits/Reservations, and DRS

**Estimated time:** 25 minutes

## Exercise

Create a resource pool with defined CPU/memory shares and a reservation, add sibling VMs and resource pools to observe share dilution, then configure a DRS anti-affinity rule to keep two VMs on separate hosts

## Key takeaway

Shares, limits, and reservations solve different resource-guarantee problems, and DRS rules must be selected based on whether the requirement is a strict enforcement or a soft preference.
