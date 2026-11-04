# Proving ground

A Claude Project that evaluates AI tools, frameworks, and agent architectures, and turns the findings into decisions a product manager can act on the same day.

Built from an agentalent.ai posting for a Tools & Frameworks Evaluator role. Company-specific detail is isolated in three knowledge files that ship as empty templates — re-platforming to a different team means filling those, not editing the instructions.

---

## Failure modes this is built against

Tool evaluation is a task where a language model is unusually dangerous, because it is fluent about exactly the things it is least reliable on. Every constraint in this package traces to one of these.

**Confident recall of stale facts.** A model will state a context window, a price, a rate limit, or a version number from training data with the same tone it uses for something it just read. In a domain where pricing changes quarterly and frameworks ship breaking changes monthly, that is the primary way an evaluation becomes actively harmful. Mitigation: the agent's own recall is defined as Tier 4 evidence and can never move a score.

**Imputed parity.** Asked to compare a well-documented tool with an opaque one, the natural move is to fill the opaque one's gaps with category assumptions. This reliably advantages the vendor who published less. Mitigation: unevidenced dimensions are excluded from the composite for both tools and the asymmetry is reported as a finding.

**Hedging dressed as rigor.** "Both have merits, it depends on your priorities" is a defensible-sounding output that transfers all the work back to the requester. It's also what a model produces by default under uncertainty. Mitigation: five fixed verdicts, no compound answers, and uncertainty expressed only as named tripwires and re-triggers.

**Post-hoc weight tuning.** Once scores exist, adjusting weights until the preferred tool wins is trivial and invisible. Mitigation: weights lock at intake, and any later change is reported under both weightings and labeled.

**Recommendation drift toward acceptance.** When success is measured by how many recommendations get acted on, the incentive is to recommend what the team already wants. Mitigation: outcome tracking in the ledger separates "acted on" from "was right," and the instructions name the drift explicitly as prohibited.

**Digest sprawl.** A weekly ecosystem digest dies when it becomes a newsletter. Mitigation: a hard cap of 7 promoted items, a rule that promotion requires a named connection to a roadmap item or ledger entry, and an explicit statement that a digest with zero promoted items is valid.

---

## Architecture

Three routed modes over a shared evidence model.

```
EVALUATE   brief intake → evidence + tiering → dimension scoring
           → integration & cost model → verdict + tripwires → delivery + ledger

MONITOR    source sweep → connection test → promote (cap 7) → also-seen → open loops

RECHECK    load prior → identify changes → re-score affected only
           → carry forward the rest → holds / weakens / flips → new recheck date
```

Seven scoring dimensions, 0–4, weighted: capability fit, maturity, integration complexity, cost shape, lock-in, governance posture, ecosystem viability. Composite is computed over scored dimensions only, with weight coverage reported alongside. Below 60% coverage, the verdict is forced to `DECISION BLOCKED`.

Every evaluation carries a volatility class that derives its recheck date. The ledger's re-triggers feed the monitor mode, which is what converts past decisions into live monitoring instead of archaeology.

---

## Files

| File | Ships |
|---|---|
| `instructions.md` | Complete — the project instruction block |
| `knowledge/scoring-rubric.md` | Complete — 7 dimensions, anchors, weights, volatility classes |
| `knowledge/evidence-tiers.md` | Complete — tiering rules, scoring floors, citation format |
| `knowledge/delivery-formats.md` | Complete — one-pager, scorecard, digest, diff |
| `knowledge/current-stack-inventory.md` | **Empty template** — fill before first use |
| `knowledge/evaluation-ledger.md` | **Empty template** — accumulates |
| `knowledge/monitoring-sources.md` | Classes complete, sources bracketed |
| `test-harness.md` | 16 scenarios, 6 release-blocking |

The three templates ship deliberately empty rather than seeded with plausible examples. Seeded examples get mistaken for real configuration and quietly corrupt the first several evaluations.

---

## Setup

1. Create a Claude Project. Paste `instructions.md` into project instructions.
2. Upload all six knowledge files.
3. Fill `current-stack-inventory.md`. Until this exists, integration scoring returns `NO EVIDENCE` on every evaluation — by design.
4. Fill `monitoring-sources.md` with actual sources and point the promotion rule at wherever the roadmap lives.
5. Run the six release-blocking harness scenarios before first real use.

Leave `evaluation-ledger.md` empty. It fills from use.

---

## Meeting the posting's success criteria

**Scorecard within 3 business days of brief.** The six-stage pipeline front-loads scope lock so evidence collection is bounded by the use case rather than the tool's full surface. Named gaps let an evaluation ship on time with its holes labeled instead of slipping while someone chases a vendor.

**≥80% of recommendations acted on or formally reviewed.** Three things drive this: the verdict is in the first line of a ≤300-word one-pager; every ADOPT/TRIAL carries tripwires that make commitment reversible; and every HOLD/PASS carries a re-trigger, which converts a "no" into a scheduled revisit rather than a dead end. `DECISION BLOCKED` is deliberately expensive to issue so it doesn't become the default.

The ledger's outcome fields track acted-on and was-right separately, because a rising acted-on rate can just mean the evaluations got safer.

---

## Patterns

Two candidates for the pattern library:

- **`absent-evidence-is-not-parity`** — in any comparative scoring system, a dimension unevidenced for one subject is excluded for all subjects rather than imputed. Prevents opacity from being rewarded and prevents documentation quality from masquerading as product quality.
- **`verdict-forcing-with-tripwires`** — uncertainty is expressed as named reversal conditions attached to a committed verdict, never as hedged prose. Makes a recommendation both decisive and revisable.

Reuses `evidence-tiered-scoring` (from the corpus decay auditor's source tiering, where Tier 3 was barred from verdicts) and the three-way-routing lineage in the five-verdict set.
