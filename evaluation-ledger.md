# Evaluation ledger

**Ships empty. Accumulates one row per completed evaluation.**

The ledger is what makes the second year of this work cheaper than the first. It answers "have we looked at this before," feeds recheck scheduling, and gives the monitor mode something to fire against.

Append only. Never overwrite an entry — a recheck adds a new row referencing the prior brief ID.

---

## Index

| Brief ID | Subject | Verdict | Composite | Coverage | Evidence as of | Recheck by | Status |
|---|---|---|---|---|---|---|---|
| [EV-YYYYMMDD-slug] | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] | [current/stale/superseded] |

---

## Entry template

```
### EV-YYYYMMDD-<slug>

Subject:        [tool, version]
Decision fed:   [what the product team decided or is deciding]
Incumbent:      [ ]
Use case:       [boundary]
Weights:        [if non-default, record them — comparisons require matching weights]
Verdict:        [ADOPT | TRIAL | HOLD | PASS | DECISION BLOCKED]
Composite:      [n.n]  Coverage: [n of 7, x%]
Volatility:     [class]
Evidence as of: [date]   Recheck by: [date]

Zero-scored dimensions: [list, or none]

Tripwires / re-trigger:
- [ ] → [consequence] | fired: [no | YYYY-MM-DD]
- [ ] → [consequence] | fired: [no | YYYY-MM-DD]

Named gaps at time of decision:
- GAP-1: [ ]

Outcome (fill in later):
- Acted on: [yes/no/partial] as of [date]
- What actually happened: [ ]
- Was the verdict right: [ ]

Supersedes: [prior brief ID, or none]
Superseded by: [ ]
```

---

## Outcome tracking

The success criterion for this role is that ≥80% of recommendations get acted on or formally reviewed. That number is only meaningful if outcomes are recorded honestly, including the ones that got ignored.

Review the outcome fields monthly. Two patterns to watch for:

- **Recommendations acted on but wrong.** Verdict quality problem. Look at which dimension was mis-scored and whether the evidence tier rules were followed.
- **Recommendations ignored.** Usually one of: the decision wasn't real, the turnaround missed the window, or the one-pager buried the verdict. All three are fixable, and all three are on this side of the table.

Do not adjust future verdicts toward what the team is likely to accept. That inflates the acted-on rate and destroys the reason the role exists.
