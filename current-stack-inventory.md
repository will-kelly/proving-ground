# Current stack inventory

**Ships empty. Fill before first use.**

This file is the only thing that makes integration scoring real rather than theoretical. If it's blank or stale, dimension 3 scores `NO EVIDENCE` — that is intended behavior, not a bug.

**Last verified:** [DATE — if older than 90 days, treat as stale and flag it]
**Owner:** [NAME/ROLE]

---

## Model and inference layer

| Component | Vendor/version | Role | Contract/commit | Notes |
|---|---|---|---|---|
| [e.g. primary LLM API] | [ ] | [ ] | [ ] | [ ] |
| [fallback / secondary] | [ ] | [ ] | [ ] | [ ] |
| [embeddings] | [ ] | [ ] | [ ] | [ ] |
| [self-hosted, if any] | [ ] | [ ] | [ ] | [ ] |

## Orchestration and agent framework

| Component | Version | What it owns | Replaceable? |
|---|---|---|---|
| [ ] | [ ] | [ ] | [ ] |

## Data layer

| Component | Version | Holds | Migration difficulty |
|---|---|---|---|
| [vector store] | [ ] | [ ] | [ ] |
| [primary DB] | [ ] | [ ] | [ ] |
| [cache/queue] | [ ] | [ ] | [ ] |

## Observability and evaluation

| Component | Covers | Gaps |
|---|---|---|
| [tracing] | [ ] | [ ] |
| [eval harness] | [ ] | [ ] |
| [cost monitoring] | [ ] | [ ] |

## Deployment and runtime

| Component | Notes |
|---|---|
| [cloud/region] | [ ] |
| [container/serverless] | [ ] |
| [CI/CD] | [ ] |
| [secrets] | [ ] |

---

## Integration seams

The places a new tool can attach without a rebuild. This section does the most work in Stage 4 — be specific.

- [SEAM 1: name, interface, what already plugs in here]
- [SEAM 2: ]

## Load-bearing components

Replacing any of these is a 0 on integration complexity. Name them so the agent can recognize the situation.

- [COMPONENT — why it's load-bearing — who owns it]

## Known constraints

Hard boundaries that make some tools non-starters regardless of score.

- [Data residency: ]
- [Deployment boundary — SaaS permitted / VPC only / self-host only: ]
- [Procurement floor — spend above which a formal process triggers: ]
- [Language/runtime constraints: ]
- [Existing contractual commits that create switching penalties: ]

## Current volumes

Needed for cost modeling. Without these, cost shape scores are directional only — say so.

- [Requests/month: ]
- [Tokens/month: ]
- [Concurrent agents at peak: ]
- [Expected 12-month growth multiple: ]
