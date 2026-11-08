# Evidence tiers

Every claim that touches a score carries a citation and a tier. Ships complete.

## The tiers

**Tier 1 — Direct measurement.**
We ran it. A benchmark we executed, a spike we built, a load test against our own workload. Requires: date, environment, reproducible steps, raw result. Outranks everything else, including vendor benchmarks that disagree.

**Tier 2 — Primary source.**
Official documentation, source code, release notes, changelog, published pricing page, DPA, SOC 2 report, security whitepaper, published benchmark *with disclosed methodology and reproducible setup*. Requires: URL and access date.

A dated check that a vendor does *not* publish something is also Tier 2. See *Checked, not published* below.

**Tier 3 — Credible secondary.**
Independent third-party benchmark, peer-reviewed paper on the underlying technique, practitioner writeup with enough detail to assess whether it resembles our workload, a named engineer's postmortem. Requires: source, date, and a one-line note on why it's credible.

**Tier 4 — Uncorroborated.**
Vendor marketing, launch blog claims, conference talks, analyst summaries without disclosed method, comparison pages published by a vendor about competitors, social posts, aggregator listicles, vendor facts supplied by the requester without a source, **and your own recall from training data**.

---

## Environment attestation

Facts about *our own* environment are a separate class from facts about a vendor. When `current-stack-inventory.md` is blank or stale, the requester can attest to the stack at intake: incumbent components, seams, load-bearing components, hard constraints, and volumes.

```
[E1] Env | Requester attestation, <name/role> | <date> | brief EV-…
```

Attestation is valid evidence for dimension 3 (integration) and for the volume inputs to dimension 4 (cost shape). It is never valid for a vendor fact. A requester saying "we run Postgres 16 with pgvector" is attestation. A requester saying "their pricing is about $40 a seat" is Tier 4. The rule that your own recall is Tier 4 applies to requester-supplied vendor facts in exactly the same way.

Any scorecard that relies on attestation says so in the header (`Stack source: requester attestation`).

---

## Scoring rules

| Rule | Effect |
|---|---|
| A dimension score requires ≥1 Tier 1–2 citation (or Env attestation for dimension 3) | Otherwise `NO EVIDENCE` |
| Tier 3 alone | Caps that dimension at 2 |
| Tier 4 | Never scores. May appear in the report, explicitly labeled `vendor claim, unverified` |
| Tier 1 conflicts with Tier 2 | Tier 1 wins; note the conflict, it's often the most useful line in the report |
| Two Tier 2 sources conflict | Report both, score conservatively, flag as a named gap |
| Checked, not published | Scores only where the rubric defines an absence anchor or cap for that dimension |
| Not checkable | `NO EVIDENCE` plus a named gap |

## Model recall is Tier 4

This is the rule that catches the most dangerous failure. Anything you believe you know about a tool, including its context window, pricing, rate limits, current version, or whether a feature shipped, is Tier 4 regardless of confidence. This applies most sharply to:

- Version numbers and release states
- Any price, quota, limit, or benchmark figure
- Feature availability ("it supports X")
- Comparative claims ("A is faster than B")
- Anything about a product released or updated recently

If it has a number in it and you didn't read it today, cite it or drop it.

---

## Two kinds of missing

Missing evidence comes in two states, and they get different treatment. Collapsing them is the error that lets an opaque vendor neutralize a transparent one.

**Checked, not published.** You looked in the places a vendor would publish the item (docs, pricing page, trust center, changelog, repo, status page) on a dated access, and it isn't there. That absence is a finding about the vendor, cited at Tier 2:

```
[C7] Tier 2 | Checked: trust center, docs, legal page | DPA not published | <urls> | accessed 2026-11-07
```

It scores against the absence anchors and caps in `scoring-rubric.md`. Where a dimension has no absence anchor, it is `NO EVIDENCE`. A missing feature list doesn't prove a missing feature, so capability fit has no absence anchor.

**Not checkable.** The evidence may exist, but you can't reach it: gated behind credentials, an NDA, a paid account, a signed contract, or the runtime has no retrieval tool. That's `NO EVIDENCE`, recorded as a named gap.

The test: could a diligent buyer find this without signing anything? If yes and it isn't there, that's *checked, not published*. If they'd need to sign or log in, it's *not checkable*.

Pricing behind "contact sales" is *checked, not published* (the vendor chose not to publish), and it scores under the dimension 4 rule. A SOC 2 report available only under NDA is *not checkable* for the report's contents. But if the trust center confirms the report exists, that confirmation is Tier 2 evidence of the attestation.

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
[C4] Tier 2 | Checked: pricing page, docs | rates not published, per-seat unit stated | <url> | accessed 2026-11-07
[E1] Env | Requester attestation, platform lead | 2026-11-07 | brief EV-20261107-example
```

Citation IDs travel into the scorecard and the ledger. A dimension score with no citation ID is a defect.

**Evidence as of** means the oldest access date among the citations behind any *scored* dimension. Citations behind `NO EVIDENCE` dimensions and Tier 4 labels don't set it.

---

## Absent evidence is not parity

When comparing tools, apply the two kinds of missing per tool, per dimension:

1. **Tool B is *checked, not published* on a dimension.** Score Tool B against the absence anchor or cap. Score Tool A normally. Nothing is excluded. Opacity is a property of the vendor, and it shows up in the score.
2. **Tool B is *not checkable* on a dimension.** Mark Tool B `NO EVIDENCE`, and exclude that dimension from the composite **for both tools**. State what the exclusion removes: "Excluding governance removes Tool A's evidenced 3."
3. **Never impute** a score from category, reputation, funding, customer logos, or similarity to a known tool.

The first rule keeps a well-documented tool from losing to an opaque one. The second keeps a tool from being punished for evidence we failed to get. The stated removal in rule 2 keeps the second rule from hiding what it costs.
