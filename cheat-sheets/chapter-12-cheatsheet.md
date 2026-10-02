## Chapter 12 Cheat Sheet: Exam Simulation & Time Management

### Exam Structure (2V0-21.23)
| Item | Value |
|---|---|
| Questions | ~70 |
| Time limit | 135 minutes |
| Scoring scale | 100-500 |
| Passing score | 300 |
| Time budget/question | ~1.5-1.9 min, leaving 15-20 min buffer |

### Time-Management Plan
1. **First pass (≈100 min):** Answer every question with your best judgment. Flag anything uncertain — never leave blank.
2. **Second pass (≈20-25 min):** Revisit flagged questions only, grouped mentally by domain to keep context loaded.
3. **Final check (≈5-10 min):** Confirm zero unanswered questions before submitting.

### Flagging Rule
Blank answer = guaranteed 0 credit. Flagged + best-guess answer = credit possible + chance to improve on revisit. Always select something before flagging.

### Elimination Technique
| Trap Type | How to Spot It |
|---|---|
| Deprecated feature | e.g., standalone VUM offered as 'current' tool → eliminate; current tool is vLCM |
| Mismatched host count | RAID-1 FTT=1 needs 3 hosts, RAID-5 needs 4, RAID-6 needs 6 — check cluster size against policy |
| Ignores stated constraint | Option technically works but violates budget, downtime, or host-count limit given in scenario |
| Overengineered answer | Sounds advanced but scenario explicitly asks for 'simplest' or 'least overhead' solution |

### Reading Scenario Questions
Before looking at options, extract:
- **Budget** (cost-sensitive vs not)
- **Downtime tolerance** (zero-downtime vs maintenance window OK)
- **Host count** (validates minimums for vSAN RAID levels, HA policies, cluster features)

### Domain Rapid-Review Order (final review pass)
Architecture → Networking → Storage → VM Management → Resource/Availability → Security/Lifecycle/Monitoring

### vSAN Storage Policy Quick Reference
| Policy | Min Hosts | Capacity Overhead | Use When |
|---|---|---|---|
| RAID-1 (FTT=1) | 3 | High | Simplicity/performance priority |
| RAID-5 (FTT=1) | 4 | Medium | All-flash, capacity matters |
| RAID-6 (FTT=2) | 6 | Medium-High | All-flash, tolerate 2 failures |

### HA Admission Control Quick Reference
| Policy | Best For |
|---|---|
| Percentage-based (auto) | Maximize usable resources, no dedicated spare |
| Dedicated failover host(s) | Predictable, isolated failover capacity |
| Slot policy | Legacy/uniform VM sizing scenarios (can over-reserve) |

### Final-Minutes Checklist
- [ ] Every question answered (no blanks)
- [ ] All flagged questions resolved with a definite choice
- [ ] Re-verified constraint-based questions (budget/downtime/host count)
- [ ] Submitted only after full review pass complete
