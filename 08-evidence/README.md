# 08 — Evidence

All implementation evidence is organized here by purpose rather than duplicated across module folders.

## Evidence Categories

- `screenshots/` — SAP GUI execution evidence
- `evidence-packs/` — curated documentation packages
- `SCREENSHOT-MANIFEST.md` — consolidated screenshot index

## Current Evidence Sets

### Plan-to-Produce / Manufacturing — Completed Through Goods Receipt

The manufacturing execution for Production Order `1000020` covers:

`OPK4 → CO15 → MIGO 101 → Material Document 5000000063 → MMBE → CO03`

Key results:

- Material `194 — TechNova Business Laptop`
- Plant / Storage Location `TN01 / FG10`
- Confirmed Yield `10 EA`
- Material Document `5000000063`
- Final unrestricted stock `95 EA`
- Final operational status includes `REL`, `CNF`, `PDLV`

The supplied 12-page execution report documents production confirmation, goods receipt, inventory realization, `OBYC` GBB-AUF troubleshooting, the `KI280` cost-element issue, and `OPK9` valuation-variant configuration. It references an 18-screenshot audit sequence.

Evidence pack: [`evidence-packs/SAP_Plan_to_Produce_Execution_Report.md`](evidence-packs/SAP_Plan_to_Produce_Execution_Report.md)

Screenshot folder: `screenshots/plan-to-produce/`

### O2C Lifecycle — Completed

`VA01 → VL01N → VL02N/PGI → VF01 → FI Posting → F-28 → FBL5N`

Key documents include Sales Order `18`, Delivery `80000029`, Material Document `4900000105`, Billing `90000037`, FI Journal Entry `9000000001`, Payment `1000000000`, and final customer balance `€0.00`.

Evidence pack: [`evidence-packs/SAP_O2C_Execution_Report.md`](evidence-packs/SAP_O2C_Execution_Report.md)

Screenshot folder: `screenshots/o2c/`

### P2P Lifecycle — Completed

`ME21N → MIGO → MIRO → MIR4/FI Verification → F-53 → Vendor Clearing`

Evidence index: [`evidence-packs/p2p-lifecycle-report.md`](evidence-packs/p2p-lifecycle-report.md)

### CO / Universal Journal

Documents the `FINS_CUST_CONS_CHK` issue, Version `0` → Ledger `0L` configuration, `PRJ_9000` / `B2K` execution, and successful validation.

### Historical SD-FI Billing Resolution

The earlier billing-resolution case remains preserved as a separate troubleshooting reference.

## Evidence Rule

Screenshots are presented as captured SAP evidence only when the corresponding image is actually available. Documentation derived from supplied case-study material is clearly distinguished from directly captured repository evidence.