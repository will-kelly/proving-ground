# Delivery formats

Ships complete. These are the only shapes output takes.

Placeholders in angle brackets are slots, not examples. Never carry a placeholder value, or any brief ID that isn't in `evaluation-ledger.md`, into a real deliverable.

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

**Evidence conflict** (omit if none)
<Tier 1 result> vs <Tier 2 claim> [<C-ids>] — scored on Tier 1.

**Confidence**
<n> of 7 dimensions scored (<x>% of weight). Composite <n.n>.
Weakest evidence: <dimension> — <why>.
Evidence as of <date>. Recheck by <date>.

*Full scorecard below.*
```

Rules:
- Never open with background on the tool. The PM either knows what it is or will ask.
- The trade-off section names what is *lost*, both ways. If you can only name upside, you haven't finished the evaluation.
- The engineer-week range must carry its assumption. A range without one is a guess wearing a suit. If the stack came from requester attestation, the assumption says so.
- A Tier 1 result that contradicts a Tier 2 source always gets the evidence conflict line. It's often the most useful sentence on the page, so it doesn't stay buried in the citations.
- "Weakest evidence" is mandatory. It's the line that makes the rest trustworthy.
- "Evidence as of" is the oldest access date among citations behind scored dimensions.

---

## Format A2 — Comparison one-pager

Use for any brief that evaluates two or more tools. Same ≤300-word limit, same rules as Format A.

```
## <Tool A> — <VERDICT> | <Tool B> — <VERDICT>

<One sentence: the pick, if the brief asks for one, and the single reason for it. If shared coverage is below 60%, say the comparison is blocked and why.>

**The trade-off**
- <What you give up by picking A>
- <What you give up by picking B>

**What it costs**
A: <n–m engineer-weeks> — <assumption> | Run cost: <current> → <10x>
B: <n–m engineer-weeks> — <assumption> | Run cost: <current> → <10x>

**Tripwires / re-triggers**
- A: <condition>
- B: <condition>

**Evidence conflict** (omit if none)
<Tier 1 result> vs <Tier 2 claim> [<C-ids>] — scored on Tier 1.

**Confidence**
Coverage: A <x>% | B <x>% | shared <x>%. Composite over shared dimensions: A <n.n> | B <n.n>.
Excluded for all: <dimension — what it removed from which tool> | none.
Opacity findings: <tool — dimension scored as checked, not published> | none.
Weakest evidence: <dimension, tool> — <why>.
Evidence as of <date>. Recheck by <date>.

*Full comparison scorecard below.*
```

The excluded-for-all and opacity lines are mandatory. They're the two places a comparison can quietly favor the vendor that published less, and the PM needs to see both.

---

## Format B — Full scorecard

```
Brief:          EV-YYYYMMDD-<slug>
Subject:        <tool> <version>
Decision:       <decision this feeds>
Incumbent:      <what it's measured against>
Use case:       <boundary>
Stack source:   <verified inventory, dated | requester attestation [E-ids] | none>
Evidence as of: <date>
Volatility:     <class>
Recheck by:     <date>
Coverage:       <n> of 7 (<x>% of weight)
Composite:      <n.n>
Verdict:        <VERDICT>
Precedence:     <which verdict-precedence rule set the verdict: 1 | 2 | 3 | 4>
```

| # | Dimension | Weight | Score | Justification | Cites | Top tier |
|---|---|---|---|---|---|---|
| 1 | Capability fit | 25 | 3 | <one line> | C1, C4 | 2 |
| … | | | | | | |
| 3 | Integration | 20 | — | NO EVIDENCE — no inventory or attestation | — | — |
| 6 | Governance | 10 | 0 | Checked, not published: no data handling terms | C7 | 2 |

Mark absence-based scores in the justification as `Checked, not published`, so a reader can tell them from positive findings.

**Cost model**
| | Current volume | 10x |
|---|---|---|
| Scales on | | |
| Est. monthly | | |
| Controls available | | |

If volumes are missing, label the model `Directional only — no volumes`.

**Exit cost**: <what accumulates here, and whether it leaves with us>

**Named gaps**
```
GAP-1: <missing> | <why> | <owner> | blocks dimension <n>
```

**Citations**
```
[C1] Tier 2 | <source> | <url> | accessed <date>
[E1] Env | Requester attestation, <role> | <date>
```

**Tripwires / re-trigger**
- <condition> → <consequence>

---

## Format B2 — Comparison scorecard

Use when a brief evaluates two or more tools. All tools share one brief ID, one set of weights, and one use case boundary.

```
Brief:            EV-YYYYMMDD-<slug>
Subjects:         <tool A version> | <tool B version>
Decision:         <decision this feeds>
Incumbent:        <what they're measured against>
Use case:         <boundary>
Stack source:     <verified inventory | requester attestation | none>
Evidence as of:   <date — oldest across all tools>
Volatility:       <most volatile class among the subjects>
Recheck by:       <date>
Coverage:         A: <n> of 7 (<x>%) | B: <n> of 7 (<x>%)
Shared coverage:  <n> of 7 (<x>%)
Excluded for all: <dimension — not checkable for <tool> — removes <tool>'s evidenced <score>> | none
Composite (shared dimensions only): A <n.n> | B <n.n>
Verdict:          <one verdict per tool, plus the pick if the brief asks for one>
```

| # | Dimension | Weight | A | B | Note |
|---|---|---|---|---|---|
| 6 | Governance | 10 | 3 [C3] | 0 [C9, checked, not published] | Scored for both. Opacity is B's finding. |
| 3 | Integration | 20 | 3 [E1] | — not checkable [GAP-2] | Excluded for both; removes A's 3. |

The "Excluded for all" line is mandatory whenever an exclusion happens. Without it, a reader can't see what the exclusion cost the better-documented tool.

---

## Format C — Weekly digest

```
# Ecosystem digest — week of <date>

**Promoted: <n> of <total candidates> reviewed**
**Sweep scope:** <full | partial — sources not configured: <classes>; roadmap location not set>

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
- <brief ID from evaluation-ledger.md> — past recheck (due <date>)
- <brief ID from evaluation-ledger.md> — awaiting <evidence> from <source>, owner: <name>
- Tripwire fired: <brief ID from evaluation-ledger.md> — <which tripwire>
- Config: <monitoring sources / roadmap location missing — owner>
```

Rules:
- Hard cap of 7 promoted items. If more qualify, cut by "does this change a decision currently on the table."
- Promotion requires a named connection. Interesting-but-unconnected is a one-line also-seen, with no commentary.
- Zero promoted items is a valid digest. Say so plainly. Don't manufacture relevance.
- "Also seen" entries get no analysis. One line, source, done.
- A partial sweep says so in the scope line. Never imply full coverage of source classes that aren't configured.
- Open loops list only brief IDs that exist in `evaluation-ledger.md`. With an empty ledger, the only open loops are configuration gaps and briefs awaiting input in this conversation.

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

---

## Format E — Ledger and inventory blocks

Ledger entries and attested stack inventories are emitted as fenced blocks at the end of the deliverable, under one of these labels:

```
LEDGER ENTRY — written to evaluation-ledger.md (<tool used>, <timestamp>)
LEDGER ENTRY — ready to append, not yet written
STACK INVENTORY (attested) — ready to paste into current-stack-inventory.md
```

Use the "written" label only after a write tool has returned success. In every other case, use "ready to append." Saying an entry is in the ledger when it isn't corrupts every later recheck.

**Appending with a write tool that replaces the whole file.** Most document write tools have no append operation. The ledger is append-only, so a careless write erases history. When the only write path replaces the full file:

1. Read `evaluation-ledger.md` in the same turn, immediately before writing.
2. Write the full current content, with the new entry added under the entry template and a new row added to the index. Change no existing entry or row.
3. Read the file back and confirm that the new entry and every prior entry are present.
4. Only then use the "written" label. If any step fails, use "ready to append" and say which step failed.
