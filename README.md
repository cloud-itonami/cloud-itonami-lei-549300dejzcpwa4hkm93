# cloud-itonami-lei-549300dejzcpwa4hkm93

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by FirstGroup plc.**

This repository archives the publicly published Terms of Use of the **First Bus**
brand (firstbus.co.uk), operated under **FirstGroup plc**, with source-url and
retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.edn)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: FirstGroup plc
- **LEI (ISO 17442)**: [549300DEJZCPWA4HKM93](https://search.gleif.org/#/record/549300DEJZCPWA4HKM93) (GLEIF-verified, status ACTIVE, registration ISSUED)
- **Jurisdiction**: GB (Scotland; company number SC157176)
- **Website**: https://www.firstgroupplc.com (archived terms from the First Bus consumer brand, firstbus.co.uk)
- **Ticker**: FGP (LSE)

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.

## Related cloud-itonami blueprint (passenger-road-transport vertical)

First Bus is one of the UK's largest urban/suburban bus operators, running local
bus networks across many UK cities and regions. This vertical's *generic,
forkable* Open Business Blueprint counterpart in the `cloud-itonami` fleet is
[`cloud-itonami-isic-4921`](https://github.com/cloud-itonami/cloud-itonami-isic-4921)
(ISIC 4921/4922 sibling pair — urban/suburban vs. intercity/chartered coach
scheduling-and-dispatch coordination, Advisor⊣Governor actor pattern). This
LEI-catalog entry is a **read-only ToS reference only** — it is not a fork of, and
has no code dependency on, isic-4921; the cross-reference exists so a reader
researching real-world urban-bus operators for market/competitive context can find
both the real company's published terms and the corresponding generic
governed-actor blueprint from one place.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`).
