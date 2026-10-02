## Chapter 12: Full Exam Simulation and Time-Management Strategy — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | 2V0-21.23 exam: question count and time limit? | ~70 questions, 135 minutes. Exam tip: budget under 2 min/question to leave buffer for flagged-question review. |
| 2 | 2V0-21.23 scoring scale and minimum passing score? | Scaled score 100-500; passing score is 300. Exam tip: raw questions aren't weighted equally, so don't count 'correct answers' — trust the scaled score. |
| 3 | Recommended time budget per question on 2V0-21.23? | ~1.5-1.9 min/question on first pass, leaving 15-20 min buffer at the end for flagged-question review. |
| 4 | vSAN RAID-1 (Mirroring) minimum host count for FTT=1? | 3 hosts. Exam tip: RAID-1 uses more capacity but has lower host requirements and simpler failure handling than erasure coding. |
| 5 | vSAN RAID-5 erasure coding minimum host count? | 4 hosts (all-flash only). Exam tip: saves capacity vs RAID-1 but requires more hosts and all-flash. |
| 6 | vSAN RAID-6 erasure coding minimum host count? | 6 hosts (all-flash only, FTT=2). Exam tip: if scenario gives a 4-host cluster, RAID-6 is automatically eliminated. |
| 7 | VUM (vSphere Update Manager) vs vLCM — which is current? | vLCM (vSphere Lifecycle Manager) is the current unified patch/upgrade/firmware tool; standalone VUM workflow is deprecated in vSphere 7/8. Exam tip: any option describing standalone VUM as the modern answer is a trap. |
| 8 | HA Admission Control: percentage-based vs dedicated failover host vs slot policy — when to pick percentage-based? | Pick percentage-based when the scenario wants automatic, non-wasteful capacity reservation without dedicating an idle host. Exam tip: 'maximize usable resources, no dedicated spare host' = percentage-based. |
| 9 | Elimination technique for scenario questions — first step? | List explicit constraints (budget, downtime tolerance, host count) BEFORE evaluating answer options. Exam tip: options are often designed to be correct only if you ignore a stated constraint. |
| 10 | Flagging strategy: when uncertain on a complex question, what should you do? | Select your current best answer, flag for review, and move on. Never leave blank — blank answers guarantee zero credit even if you never revisit it. |
| 11 | Domain-by-domain rapid review order for final pass? | Architecture → Networking → Storage → VM Management → Resource/Availability → Security/Lifecycle/Monitoring. Exam tip: review flagged questions grouped by domain to keep context fresh. |
| 12 | Final-minutes checklist before submitting the exam? | 1) Confirm no question is left unanswered. 2) Resolve all flagged questions with a definite selection. 3) Re-check any question where you second-guessed constraints (budget/downtime/host count). 4) Submit only after all 70 are answered. |
