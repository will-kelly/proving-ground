# Proving ground

A Claude Project that evaluates AI tools, frameworks, and agent architectures, and turns the findings into decisions a product manager can act on the same day.

Built from an agentalent.ai posting for a Tools & Frameworks Evaluator role. Company-specific detail is isolated in three knowledge files that ship as empty templates. Re-platforming to a different team means filling those, not editing the instructions.

---

## Failure modes this is built against

Tool evaluation is a task where a language model is unusually dangerous, because it's fluent about exactly the things it's least reliable on. Every constraint in this package traces to one of these.

**Confident recall of stale facts.** A model will state a context window, a price, a rate limit, or a version number from training data in the same tone it uses for something it just read. In a domain where pricing changes quarterly and frameworks ship breaking changes monthly, that's the main way an evaluation becomes actively harmful. Mitigation: the agent's own recall is defined as Tier 4 evidence and can never move a score.

**Imputed parity.** Asked to compare a well-documented tool with an opaque one, the natural move is to fill the opaque one's gaps with category assumptions. That reliably advantages the vendor who published less. Mitigation: the agent separates "checked, not published" from "not checkable." A vendor that chose not to publish its data handling terms scores on that choice. Evidence we simply couldn't reach is excluded for every tool in the comparison, and the report states what the exclusion cost the better-documented one.

**Hedging dressed as rigor.** "Both have merits, it depends on your priorities" sounds defensible and hands all the work back to the requester. It's also what a model produces by default under uncertainty. Mitigation: five fixed verdicts, a published precedence order for picking among them, no compound answers, and uncertainty expressed only as named tripwires and re-triggers.

**Post-hoc weight tuning.** Once scores exist, adjusting weights until the preferred tool wins is trivial and invisible. Mitigation: weights lock at intake, and any later change is reported under both weightings and labeled.

**Recommendation drift toward acceptance.** When success is measured by how many recommendations get acted on, the incentive is to recommend what the team already wants. Mitigation: outcome tracking in the ledger separates "acted on" from "was right," and the instructions name the drift explicitly as prohibited.

**Phantom record-keeping.** An agent asked to "add it to the ledger" will often say it did, whether or not it has a write path. Every later recheck then rests on a record that doesn't exist. Mitigation: ledger entries are emitted as labeled blocks, and the "written" label requires a successful write and a read-back.

**Digest sprawl.** A weekly ecosystem digest dies when it becomes a newsletter. Mitigation: a hard cap of 7 promoted items, a rule that promotion requires a named connection to a roadmap item or ledger entry, and an explicit statement that a digest with zero promoted items is valid.

---

## Architecture

Three routed modes over a shared evidence model.

```
EVALUATE   brief intake (+ stack attestation if needed) → retrieval check
           → evidence + tiering → dimension scoring → integration & cost model
           → verdict (precedence order) + tripwires → delivery + ledger block

MONITOR    source sweep (full or partial) → connection test → promote (cap 7)
           → also-seen → open loops

RECHECK    load prior (or ask for it) → identify changes → re-score affected only
           → carry forward the rest → holds / weakens / flips → new recheck date
```

Seven scoring dimensions, 0–4, weighted: capability fit, maturity, integration complexity, cost shape, lock-in, governance posture, and ecosystem viability. The composite is computed over scored dimensions only, with weight coverage reported alongside. Below 60% coverage, the verdict is `DECISION BLOCKED`, unless an evidenced capability gap or a violated hard constraint has already settled it as `PASS`.

Every evaluation carries a volatility class that sets its recheck date. The ledger's re-triggers feed the monitor mode, which turns past decisions into live monitoring instead of archaeology.

---

## Files

| File | Where it goes | Ships |
|---|---|---|
| `instructions.md` | Paste into the Project's instructions field | Complete |
| `scoring-rubric.md` | Project knowledge | Complete: 7 dimensions, anchors, absence rules, weights, verdict precedence, volatility classes |
| `evidence-tiers.md` | Project knowledge | Complete: tiering, the two kinds of missing, environment attestation, citation format |
| `delivery-formats.md` | Project knowledge | Complete: one-pager, comparison one-pager, scorecard, comparison scorecard, digest, diff, ledger blocks and append procedure |
| `current-stack-inventory.md` | Project knowledge | **Empty template.** Fill before first use, or let intake fill it by attestation |
| `evaluation-ledger.md` | Project knowledge | **Empty template.** Accumulates |
| `monitoring-sources.md` | Project knowledge | Classes complete, sources bracketed |
| `test-harness.md` | **Repo only, not the Project** | 32 scenarios, 7 release-blocking, plus a run protocol and run log |

The three templates ship deliberately empty rather than seeded with plausible examples. Seeded examples get mistaken for real configuration and quietly corrupt the first several evaluations. The same rule applies to the format examples: placeholders are slots, never brief IDs an agent could mistake for real records.

The test harness stays out of the Project. If the agent can read the pass criteria, the harness tests whether it read the answer key. For the same reason, no Project file refers to harness scenario IDs.

---

## Setup

1. Create a Claude Project. Paste `instructions.md` into the project instructions.
2. Upload the six knowledge files. Don't upload `test-harness.md`.
3. Fill `current-stack-inventory.md` if you can. If you can't, the agent asks for the essentials at intake and emits an attested inventory block for you to paste in.
4. Fill `monitoring-sources.md` and point the promotion rule at wherever the roadmap lives. Until then, the digest runs a labeled partial sweep.
5. Decide where ledger entries land. If the runtime can write to `evaluation-ledger.md`, the agent appends using the read, write, read-back procedure. If not, someone pastes the emitted block after each evaluation.
6. Run the seven release-blocking harness scenarios before first real use, one fresh chat per scenario. Log the run in the harness run log.

Leave `evaluation-ledger.md` empty. It fills from use.

---

## Meeting the posting's success criteria

**Scorecard within 3 business days of brief.** The six-stage pipeline front-loads scope lock, so evidence collection is bounded by the use case rather than the tool's full surface. Named gaps let an evaluation ship on time with its holes labeled, instead of slipping while someone chases a vendor.

**≥80% of recommendations acted on or formally reviewed.** Three things drive this. The verdict is in the first line of a one-pager of 300 words or fewer. Every ADOPT or TRIAL carries tripwires that make commitment reversible. Every HOLD or PASS carries a re-trigger, which turns a "no" into a scheduled revisit rather than a dead end. `DECISION BLOCKED` is deliberately expensive to issue, so it doesn't become the default.

The ledger's outcome fields track acted-on and was-right separately, because a rising acted-on rate can just mean the evaluations got safer.
