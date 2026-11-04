# Delivery formats

Ships complete. These are the only shapes output takes.

---

## Format A — PM one-pager

The deliverable. ≤300 words. Verdict in the first line, before any context.

```
## <Tool> — <VERDICT>

<One sentence: the verdict and the single reason for it.>

**The trade-off**
- <What you give up by doing this>
- <What you give up by not doing this>
- <The third thing, if it's real — omit if it isn't>

**What it costs**
Integration: <n–m engineer-weeks> — <the assumption driving the range>
Run cost: <shape at current volume> → <shape at 10x>

**Tripwires** (reverse this decision if:)
- <Specific, observable condition>
- <Specific, observable condition>

**Confidence**
<n> of 7 dimensions scored (<x>% of weight). Composite <n.n>.
Weakest evidence: <dimension> — <why>.
Evidence as of <date>. Recheck by <date>.

*Full scorecard below.*
```

Rules:
- Never open with background on the tool. The PM either knows what it is or will ask.
- The trade-off section names what is *lost*, both ways. If you can only name upside, you haven't finished the evaluation.
- The engineer-week range must carry its assumption. A range without one is a guess wearing a suit.
- "Weakest evidence" is mandatory. It's the line that makes the rest trustworthy.

---

## Format B — Full scorecard

```
Brief:          EV-YYYYMMDD-<slug>
Subject:        <tool> <version>
Decision:       <decision this feeds>
Incumbent:      <what it's measured against>
Use case:       <boundary>
Evidence as of: <date>
Volatility:     <class>
Recheck by:     <date>
Coverage:       <n> of 7 (<x>% of weight)
Composite:      <n.n>
Verdict:        <VERDICT>
```

| # | Dimension | Weight | Score | Justification | Cites | Top tier |
|---|---|---|---|---|---|---|
| 1 | Capability fit | 25 | 3 | <one line> | C1, C4 | 2 |
| … | | | | | | |
| 3 | Integration | 20 | — | NO EVIDENCE — stack inventory stale | — | — |

**Cost model**
| | Current volume | 10x |
|---|---|---|
| Scales on | | |
| Est. monthly | | |
| Controls available | | |

**Exit cost**: <what accumulates here, and whether it leaves with us>

**Named gaps**
```
GAP-1: <missing> | <why> | <owner> | blocks dimension <n>
```

**Citations**
```
[C1] Tier 2 | <source> | <url> | accessed <date>
```

**Tripwires / re-trigger**
- <condition> → <consequence>

---

## Format C — Weekly digest

```
# Ecosystem digest — week of <date>

**Promoted: <n> of <total candidates> reviewed**

### 1. <Headline, factual, no adjectives>
What happened: <one sentence> [C1, Tier 2]
Touches: <roadmap item / brief ID / ledger entry>
Action: <NO ACTION | WATCH | TRIGGERS RECHECK of EV-… | WARRANTS NEW BRIEF>

### 2. …

---
**Also seen** (no roadmap connection)
- <one line> — <source>
- <one line> — <source>

---
**Open loops**
- EV-20260612-langgraph — past recheck (due 2026-07-27)
- EV-20260820-vectordb — awaiting pricing from vendor, owner: <name>
- Tripwire fired: <ledger entry> — <which tripwire>
```

Rules:
- Hard cap of 7 promoted items. If more qualify, cut by "does this change a decision currently on the table."
- Promotion requires a named connection. Interesting-but-unconnected is a one-line also-seen, with no commentary.
- Zero promoted items is a valid digest. Say so plainly. Do not manufacture relevance.
- "Also seen" entries get no analysis. One line, source, done.

---

## Format D — Recheck diff

```
# Recheck: <tool> — EV-YYYYMMDD-<slug>

Prior: <date> | composite <n.n> | verdict <VERDICT>
Now:   <date> | composite <n.n> | verdict <VERDICT> — **<HOLDS | WEAKENS | FLIPS>**

**What changed**
- <change> [C-new] → moved dimension <n>: <old> → <new>

**Carried forward** (unchanged, original evidence dates)
- Dimension <n>: <score> — evidence as of <original date>

**Verdict**
<If FLIPS: lead with the flip and the cause. Do not re-litigate the original.>

New recheck by: <date>
```

Never reissue a full evaluation in recheck mode. If more than half the dimensions need re-scoring, or any carried score is older than two volatility windows, escalate it to a fresh brief instead.
