# Monitoring sources

**Source classes ship complete. Specific sources ship as brackets — fill before first digest.**

The class structure is the reusable part. What goes in each class is company-specific and should be revisited quarterly.

---

## Class 1 — Vendor release channels (Tier 2)

Changelogs and release notes for anything in the current stack, plus anything with a live `HOLD` or `TRIAL` verdict in the ledger. These produce the highest-signal items because they map directly to existing decisions.

- [VENDOR — changelog/release notes URL]
- [VENDOR — ]
- [VENDOR — ]

Check: weekly.

## Class 2 — Framework repositories (Tier 2)

Release tags, deprecation notices, and major issue threads for frameworks under evaluation or in use.

- [REPO — ]
- [REPO — ]

Check: weekly. Watch for breaking changes and maintainer-departure signals.

## Class 3 — Model releases and capability shifts (Tier 2)

Provider announcement channels and model cards. A model release only gets promoted if it touches a named roadmap item — new frontier models are interesting every week and roadmap-relevant considerably less often.

- [PROVIDER — ]
- [PROVIDER — ]

Check: weekly.

## Class 4 — Research (Tier 3)

Papers on techniques directly relevant to the product direction. Filter hard. A paper is promotable only when it changes what's buildable or invalidates an assumption in a live ledger entry.

- [ARXIV CATEGORY / LIST — ]
- [CONFERENCE / VENUE — ]

Check: weekly, skim-level.

## Class 5 — Competitor and market moves (Tier 3–4)

Product launches, pricing changes, and positioning shifts from named competitors.

- [COMPETITOR — ]
- [COMPETITOR — ]

Check: weekly. Most of this is Tier 4 and lands in "also seen." Pricing changes are the exception — those are often Tier 2 and often promotable.

## Class 6 — Practitioner signal (Tier 3)

Named engineers publishing implementation detail. Value is in postmortems and migration writeups, not in opinion.

- [SOURCE — ]
- [SOURCE — ]

Check: weekly.

---

## Promotion rule

An item is promoted only if it maps to one of:
- A named roadmap item — [WHERE DOES THE ROADMAP LIVE: ]
- An open brief ID
- A ledger entry with a live tripwire or re-trigger

Everything else is a one-line "also seen." No commentary, no speculation about future relevance.

Cap: 7 promoted items per digest.

## Standing re-triggers

Pulled from ledger entries with `HOLD` or `PASS` verdicts. These are the specific things the digest is watching for on behalf of past decisions.

| Brief ID | Re-trigger | Source class to watch | Fired? |
|---|---|---|---|
| [EV-…] | [specific condition] | [class n] | [no] |

Review this table at the start of every digest. It is the main reason the digest is worth reading — it converts old decisions into live monitoring rather than archaeology.

## Sources deliberately excluded

Record what was considered and dropped, so it doesn't get re-added quarterly.

- [SOURCE — reason: too much volume / low signal / vendor-controlled / duplicated by another class]
