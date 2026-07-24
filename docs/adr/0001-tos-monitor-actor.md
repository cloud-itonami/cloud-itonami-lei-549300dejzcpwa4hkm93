# ADR-0001: ToSMonitor-LLM ⊣ ToSArchiveGovernor -- a governed actor layered on this archive

- Status: Accepted (2026-07-24)
- Related: [`com-junkawasaki/root` ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.edn)
  (the archive-only design this repo was created under -- unchanged by this
  ADR); [`com-junkawasaki/root` ADR-2607241900](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607241900-cloud-itonami-lei-tos-monitor-actor-pilot.edn)
  (the original 1-repo pilot, on `cloud-itonami-lei-2572ibtt8cczw6au4141`,
  P&G); [`com-junkawasaki/root` ADR-2607242400](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607242400-cloud-itonami-lei-tos-monitor-actor-batch10-round3.edn)
  (the 10-repo validation batch this repo is part of).

## Context

This repository archives the publicly published Terms of Use of FirstGroup
plc, per ADR-2607110300 -- a read-only reference archive. As part of a
10-repo validation batch extending the
`cloud-itonami-lei-2572ibtt8cczw6au4141` pilot (see ADR-2607241900/
ADR-2607242400 for the full fleet-level design rationale), this repo gains a
governed actor layer on top of the unchanged archive.

The LEI-registered legal entity is FirstGroup plc, but the archived document
itself is the Terms of Use of **First Bus**, one of FirstGroup's UK bus
operating brands, published on `firstbus.co.uk` rather than the parent
group's own corporate site (`firstgroupplc.com`). This is exactly what the
real archive already reflects (`80-data/public/tos.journal.edn`'s
`:tos/source-url` is `https://www.firstbus.co.uk/terms-use`) -- this ADR is
describing the existing archived data, not inventing a new source. This
actor's own fixture/demo data (`tosmonitor.store`) follows suit and uses the
First Bus site as the company's `:website`, so that the archived
`:source-url` and the fixture `:website` land on the same base domain for
this actor's own `source-domain-mismatch-violations` governor check (see
below and `tosmonitor.registry`'s ns docstring on its `.co.uk`/`.co.jp`
two-part-TLD limitation).

## Decision

Identical design and code to the pilot and every other repo in this batch
(`src/tosmonitor/{governor,phase,operation,registry,advisor}.cljc` are
byte-for-byte identical across all of them) -- see ADR-2607241900 for the
full rationale of each of the six HARD governor checks, the single
always-escalate `:tos/change-proposal` actuation, and the mock-advisor-only
scope. Only `tosmonitor.store`'s company/baseline demo data is specific to
this repo:

- **Company**: FirstGroup plc, LEI 549300DEJZCPWA4HKM93. The actor's own
  demo/test fixture uses `:website "https://www.firstbus.co.uk"` (the First
  Bus operating-brand site where the actual archived Terms of Use text
  lives), not `https://www.firstgroupplc.com` (the parent group's corporate
  site) -- see Context above.
- **Baseline provenance** (real, from this repo's own `80-data/public/
  tos.journal.edn`): source-url `https://www.firstbus.co.uk/terms-use`,
  retrieved-at `2026-07-19T07:42:47Z`, doc-type `:terms-of-service`.
- **Baseline full text**: a short, hand-written representative excerpt (not
  the real, nav-menu-heavy archived page), with a self-consistent SHA-256
  computed from that excerpt itself -- matching the pilot's own convention
  (ADR-2607241900), not a claim that this is the verbatim archived text.

The archive-of-record (`80-data/public/tos.journal.edn`) is never touched;
`commit-record!` only writes to this actor's own Store.

## Consequences

Same as the pilot (ADR-2607241900) and the batch (ADR-2607242400) --
proves the actor pattern holds for a company whose LEI-registered legal
entity and archived document happen to live on two different (brand vs.
group) domains, which is exactly the case this actor's
`source-domain-mismatch-violations` check's own documented `.co.uk`/`.co.jp`
two-part-TLD limitation anticipates.

## Run

```bash
clojure -M:dev:run     # walk a clean lifecycle + all six HARD-hold checks + a phase-0 hold + a backend swap
clojure -M:dev:test    # governor contract · phase invariants · store parity · advisor smoke
clojure -M:lint        # clj-kondo (errors fail; CI mirrors this)
```
