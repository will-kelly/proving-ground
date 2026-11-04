# Evidence tiers

Every claim that touches a score carries a citation and a tier. Ships complete.

## The tiers

**Tier 1 — Direct measurement.**
We ran it. A benchmark we executed, a spike we built, a load test against our own workload. Requires: date, environment, reproducible steps, raw result. Outranks everything else, including vendor benchmarks that disagree.

**Tier 2 — Primary source.**
Official documentation, source code, release notes, changelog, published pricing page, DPA, SOC 2 report, security whitepaper, published benchmark *with disclosed methodology and reproducible setup*. Requires: URL and access date.

**Tier 3 — Credible secondary.**
Independent third-party benchmark, peer-reviewed paper on the underlying technique, practitioner writeup with enough detail to assess whether it resembles our workload, a named engineer's postmortem. Requires: source, date, and a one-line note on why it's credible.

**Tier 4 — Uncorroborated.**
Vendor marketing, launch blog claims, conference talks, analyst summaries without disclosed method, comparison pages published by a vendor about competitors, social posts, aggregator listicles, **and your own recall from training data**.

---

## Scoring rules

| Rule | Effect |
|---|---|
| A dimension score requires ≥1 Tier 1–2 citation | Otherwise `NO EVIDENCE` |
| Tier 3 alone | Caps that dimension at 2 |
| Tier 4 | Never scores. May appear in the report, explicitly labeled `vendor claim, unverified` |
| Tier 1 conflicts with Tier 2 | Tier 1 wins; note the conflict, it's often the most useful line in the report |
| Two Tier 2 sources conflict | Report both, score conservatively, flag as a named gap |

## Model recall is Tier 4

This is the rule that catches the most dangerous failure. Anything you believe you know about a tool — its context window, its pricing, its rate limits, its current version, whether a feature shipped — is Tier 4 regardless of confidence. This applies most sharply to:

- Version numbers and release states
- Any price, quota, limit, or benchmark figure
- Feature availability ("it supports X")
- Comparative claims ("A is faster than B")
- Anything about a product released or updated recently

If it has a number in it and you didn't read it today, cite it or drop it.

## Named gaps

When evidence can't be obtained, record it rather than routing around it:

```
GAP-<n>: <what's missing> | <why unobtainable> | <who could get it> | <which dimension it blocks>
```

Named gaps appear in the scorecard. Three or more gaps on high-weight dimensions is itself a finding, and usually points toward `DECISION BLOCKED`.

## Citation format

```
[C1] Tier 2 | Official docs, "Rate limits" | <url> | accessed 2026-09-01
[C2] Tier 1 | Internal spike, 500 concurrent agents, staging | 2026-08-28 | steps: <ref>
[C3] Tier 4 | Vendor launch post claim: "10x faster" | <url> | NOT SCORED
```

Citation IDs travel into the scorecard and the ledger. A dimension score with no citation ID is a defect.

## Absent evidence is not parity

When comparing tools, if one has evidence on a dimension and the other doesn't:

1. Mark the unevidenced tool `NO EVIDENCE` on that dimension
2. Exclude the dimension from the composite **for both tools**
3. Note the asymmetry explicitly in the report

Never impute a score from category, reputation, or similarity to a known tool. A well-documented tool should not lose to an opaque one because the opaque one got the benefit of the doubt — and the reverse is the more common failure.
