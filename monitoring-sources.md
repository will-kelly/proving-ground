# Monitoring sources

**Source classes ship complete. Specific sources ship as brackets. Fill them before the first digest.**

The class structure is the reusable part. What goes in each class is company-specific and should be revisited quarterly.

---

## Running before this file is filled

If source lists are still bracketed or the roadmap location is blank, MONITOR still runs, but on a partial sweep:

1. Sweep only what's connected to something real: vendors and repos named in the ledger, open brief IDs, and standing re-triggers.
2. Mark the digest `Sweep scope: partial`, and name the unconfigured classes.
3. With no roadmap location, only brief IDs and ledger entries can justify a promotion. Say so.
4. List "monitoring sources / roadmap location not configured" under open loops, with an owner if one is known.

Don't fill an unconfigured class with sources you picked yourself. Choosing what the team watches is configuration, and configuration belongs to the team.

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

Provider announcement channels and model cards. A model release only gets promoted if it touches a named roadmap item. New frontier models are interesting every week and roadmap-relevant considerably less often.

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

Check: weekly. Most of this is Tier 4 and lands in "also seen." Pricing changes are the exception. Those are often Tier 2 and often promotable.

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

Review this table at the start of every digest. It's the main reason the digest is worth reading. It turns old decisions into live monitoring rather than archaeology.

## Sources deliberately excluded

Record what was considered and dropped, so it doesn't get re-added every quarter.

- [SOURCE — reason: too much volume / low signal / vendor-controlled / duplicated by another class]
