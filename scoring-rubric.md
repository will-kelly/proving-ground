# Scoring rubric

Seven dimensions, 0–4 each. Ships complete — this is the methodology, not client configuration.

## Weight defaults

| Dimension | Default weight |
|---|---|
| 1. Capability fit | 25 |
| 2. Maturity and stability | 15 |
| 3. Integration complexity | 20 |
| 4. Cost shape | 15 |
| 5. Lock-in and exit cost | 10 |
| 6. Governance and security posture | 10 |
| 7. Ecosystem and vendor viability | 5 |

Total: 100. Briefs may override. Weights lock at Stage 1.

Common overrides worth suggesting at intake:
- Regulated or customer-data workload → governance to 20, capability to 20
- Exploratory / pre-PMF → maturity to 10, lock-in to 5, capability to 30
- Replacing an incumbent under contract → lock-in to 20, cost shape to 20

---

## Dimension 1 — Capability fit

Against the use case boundary in the brief, not the tool's full surface.

| Score | Anchor |
|---|---|
| 0 | Cannot do the job. Missing a required primitive. |
| 1 | Does part of the job; the gap requires significant custom work. |
| 2 | Does the job with known workarounds or degraded behavior at the edges. |
| 3 | Does the job cleanly. Edges are documented and acceptable. |
| 4 | Does the job cleanly and removes work we currently do elsewhere. |

Scoring note: a 4 requires evidence of the *removal*, not just the capability.

## Dimension 2 — Maturity and stability

| Score | Anchor |
|---|---|
| 0 | Pre-release, or breaking changes with no deprecation policy. |
| 1 | Active breaking changes; API surface moved within the last quarter. |
| 2 | Stabilizing. Versioned, but deprecation windows are short or informal. |
| 3 | Stable major version, published deprecation policy, predictable cadence. |
| 4 | Stable, with evidence of backward compatibility held across at least one major version. |

Evidence sources: changelog, release tags, deprecation policy, issue backlog age distribution. Absence of a public changelog caps this at 2.

## Dimension 3 — Integration complexity

Scored against `current-stack-inventory.md`. If the inventory is empty or stale, this dimension is `NO EVIDENCE` — do not score integration against an imagined environment.

| Score | Anchor |
|---|---|
| 0 | Requires replacing a load-bearing component of the current stack. |
| 1 | Multi-team effort; changes to more than two named components. |
| 2 | Single-team effort; a wrapper or adapter layer is required. |
| 3 | Drops into an existing seam. Config and light glue. |
| 4 | Native fit with something already deployed. |

Always pair the score with the engineer-week range and the assumption driving it.

## Dimension 4 — Cost shape

Not the sticker price. The curve.

| Score | Anchor |
|---|---|
| 0 | Cost scales on a dimension we cannot control or predict. |
| 1 | Cost scales superlinearly with our expected growth vector. |
| 2 | Cost scales linearly with usage; predictable but unbounded. |
| 3 | Predictable, with usable controls (caps, tiers, budgets, alerts). |
| 4 | Predictable, controllable, and lower than the incumbent at projected 12-month volume. |

Always model at current volume and at 10x. Undisclosed pricing caps this at 2 and is reported as a finding.

## Dimension 5 — Lock-in and exit cost

| Score | Anchor |
|---|---|
| 0 | Proprietary formats for the assets we'd invest in most; no export. |
| 1 | Export exists but is lossy or undocumented. |
| 2 | Portable data, proprietary orchestration. Rebuild required to leave. |
| 3 | Open formats or a documented migration path. Weeks to leave. |
| 4 | Standards-based; substitutable behind an interface we already own. |

Ask specifically: where would twelve months of our own work accumulate, and does it come with us?

## Dimension 6 — Governance and security posture

You report posture. You do not clear a tool for compliance — that escalates.

| Score | Anchor |
|---|---|
| 0 | No published data handling terms, or terms that conflict with our obligations. |
| 1 | Terms published but material gaps (training on customer data, no regional controls, no DPA). |
| 2 | Adequate terms; no third-party attestation. |
| 3 | Published terms plus attestation (SOC 2 Type II, ISO 27001), deployment options that fit our boundary. |
| 4 | The above plus controls we can verify ourselves (self-host, BYOK, audit logging, retention config). |

## Dimension 7 — Ecosystem and vendor viability

| Score | Anchor |
|---|---|
| 0 | Single maintainer, no funding signal, declining activity. |
| 1 | Thin ecosystem; support depends on one channel. |
| 2 | Real community; documentation is uneven. |
| 3 | Healthy ecosystem, good docs, multiple integration paths, credible commercial backing. |
| 4 | The above plus meaningful adoption at organizations with our constraints. |

Do not score this on hype volume. Stars, funding announcements, and launch-week attention are Tier 4.

---

## Composite

```
composite = Σ(score × weight) / Σ(weight)   [scored dimensions only]
coverage  = Σ(weight of scored dimensions) / 100
```

Report composite to one decimal. Report coverage as a percentage and as `n of 7`.

**Coverage < 60% forces `DECISION BLOCKED`.** No exceptions.

Composite is a summary, not the verdict. A 3.1 composite with a 0 on capability fit is a `PASS`, not a strong performer. Any dimension scoring 0 must be addressed explicitly in the verdict line.

---

## Volatility classes and recheck intervals

| Class | Applies to | Recheck |
|---|---|---|
| Volatile | Frontier model APIs, pre-1.0 agent frameworks, anything under 12 months old, anything with pricing changed in the last quarter | 45 days |
| Moving | Post-1.0 frameworks with active roadmaps, established SaaS shipping quarterly | 90 days |
| Stable | Mature infrastructure, standards, protocols, tools with 2+ years of stable major version | 180 days |

When in doubt, classify more volatile. The cost of an unnecessary recheck is an hour. The cost of a stale recommendation is a roadmap quarter.
