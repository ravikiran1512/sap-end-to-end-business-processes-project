# 08 — Evidence

All implementation evidence is centralized here. There is **one evidence area only**; legacy top-level evidence folders have been retired.

## Evidence Categories

- `screenshots/` — SAP GUI execution evidence, organized by business process
- `evidence-packs/` — consolidated implementation evidence summaries
- `SCREENSHOT-MANIFEST.md` — single screenshot index

## Current Evidence Sets

### P2P Lifecycle — Completed

`ME21N → MIGO → MIRO → MIR4/FI Verification → F-53 → Vendor Clearing`

Key documents: PO `4500000149`, Material Document `5000000062`, Logistics Invoice `5105600101`, FI Document `5100000000`, Payment Document `5000000000`.

Evidence pack: [`evidence-packs/p2p-lifecycle-report.md`](evidence-packs/p2p-lifecycle-report.md)

Screenshots: [`screenshots/p2p/`](screenshots/p2p/)

### CO / Universal Journal

Documents the `FINS_CUST_CONS_CHK` issue, Version `0` → Ledger `0L`, `PRJ_9000` / `B2K` execution, and successful validation.

### MM Inbound Logistics

Documents PO `4500000149`, MIGO Movement Type `101`, and Material Document `5000000062`.

### SD-FI / O2C

Documents billing release, account determination, FI posting, customer open item, incoming payment, and clearing.

## Evidence Rule

Screenshots are presented as captured SAP evidence only when the corresponding image is actually available. Documentation derived from supplied case-study material is clearly distinguished from directly captured repository evidence.

## Navigation Principle

Evidence is organized by **business process**, not duplicated by SAP module. This keeps the portfolio easy to navigate while preserving the technical detail needed for implementation and interview review.