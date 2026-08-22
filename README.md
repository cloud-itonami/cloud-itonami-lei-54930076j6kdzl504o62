# cloud-itonami-lei-54930076j6kdzl504o62

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by iHeartCommunications, Inc..**

This repository archives publicly published legal/policy documents of
**iHeartCommunications, Inc.**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: iHeartCommunications, Inc.
- **LEI (ISO 17442)**: [54930076J6KDZL504O62](https://search.gleif.org/#/record/54930076J6KDZL504O62) (GLEIF-verified)
- **Jurisdiction**: US-TX
- **Website**: https://www.iheart.com

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived documents, each entry
  carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`, `:tos/sha256`,
  `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `facts.edn` — 9 verified registry facts with per-fact provenance. **Generated** — see below.
- `scripts/verify-facts.cljs` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.

## Verifying the record

The LEI claims above used to be assertions with nothing in the repository behind
them. `facts.edn` now carries them as data, and every value in it was read out of
a public registry response whose URL and retrieval time sit next to the value:

```
nbb scripts/verify-facts.cljs           # check the recorded facts against the live sources
nbb scripts/verify-facts.cljs --write   # re-fetch and rewrite facts.edn
```

Nine GLEIF/ISO responses back the file — the LEI record (entity **ACTIVE**,
registration **LAPSED**; the two are different fields and are recorded
separately), its 24 ISINs (counted from `meta.pagination.total`), its managing
LOU and LEI-issuer accreditation (Bloomberg Finance L.P.), registration
authority `RA000637` (Corporations Section, Texas Secretary of State, filing
`0034084400`), ISO 20275 legal form `C5K7` (US-TX For-Profit Corporation),
reporting exceptions at both consolidation levels (`NO_LEI`), and a measured
zero direct children. All nine answered `200` when the file was written; the
`direct-parent` and `ultimate-parent` endpoints answered `404` because GLEIF
publishes the exception side of that pair for this entity, which the checker
treats as a fact rather than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the
live sources, `1` a citation broke or a fact drifted, `3` the check could not be
performed at all — an absent `facts.edn`, or every request failing at the
transport level. A check that could not run must not be indistinguishable from a
check that ran and found nothing, so it refuses to report a pass rather than
exiting 0.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
