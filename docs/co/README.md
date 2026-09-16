# Controlling (CO)

## 1. CO Implementation Status

The CO workstream has progressed from foundational Controlling Area / ledger alignment and Universal Journal prerequisites into executed manufacturing-order integration and period-end settlement for Company Code / Controlling Area `9000`.

Additional CO master data, allocations, planning, and management-accounting scenarios remain future scope, but the documented production-order CO-PC close is now complete.

## 2. Controlling Area & Ledger Version Alignment

### Issue Diagnosed

The financial customizing consistency check `FINS_CUST_CONS_CHK` returned:

```text
The version 0 of CO area 9000 is not assigned to any ledger
```

### Resolution

**IMG Path:** `Controlling → General Controlling → Organization → Define Ledger for CO Version`

**Table:** `FINSC_CMP_VERSNC`

| Field | Value |
|---|---|
| Controlling Area | `9000` — TechNova Mfg. GmbH |
| CO Version | `0` — Plan/Actual Version |
| Ledger | `0L` — Leading Ledger / Legal Valuation |

The configuration was saved and validated; the blocking version-to-ledger assignment error was cleared.

## 3. Mass Data Project `PRJ_9000` — Cockpit B2K

Posting simulation `FINS_CUST_CONS_CHK_P` subsequently returned:

```text
Mass data project PRJ_9000 not yet completed: Posting is not allowed (9000 / 0L)
```

The subsequent assignment project was executed through the documented IMG activity:

`Controlling → General Controlling → Organization → Subsequent Assignment of Company Codes → Run Project for Updating Existing Journal Entries`

- Mass Data Project: `PRJ_9000`
- Activity: `B2K` — Assign Company Code to Controlling Area
- Company Code: `9000`
- Ledger: `0L`
- Errors: `0`
- Warnings: `0`

The posting block was removed successfully.

## 4. Universal Journal Integration Context

```text
Controlling Area 9000
        ↓
CO Version 0
        ↓
Ledger 0L
        ↓
Universal Journal / ACDOCA Context
        ↓
Financial Posting Validation
```

## 5. Manufacturing CO Integration

The completed Plan-to-Produce scenario extends CO integration into production execution:

```text
Production Order 1000020
        ↓
CO15 — 10 EA Confirmation
        ↓
MIGO — Goods Receipt 101
        ↓
Material Document 5000000063
        ↓
MMBE — 95 EA Unrestricted Stock
        ↓
CO03 — Production Order Validation
```

The manufacturing scenario required resolution of `KI280` cost-element compatibility, `OBYC` GBB-AUF account determination, and `OPK9` valuation-variant configuration.

## 6. Manufacturing Period-End Controlling Close — Completed

Production Order `1000020` was subsequently processed for the documented Period `09/2026` close.

### Variance Assessment — `KKS2`

The initial execution returned `KV 017: No orders (order items) could be processed`. The documented scenario proceeded through the applicable production-order settlement path using `TECO` / `SETC` and `KO88`.

### Settlement Number Range — `CO_ABRECHN`

`KO88` initially returned `KD522`. Controlling Area `9000` was assigned to the active settlement number-range group containing interval `01` (`0100000000–0199999999`).

### Price Difference Account — `OBYC / PRD`

`KO88` subsequently returned `M8147` for missing `BKMG PRD` account determination. `OBYC → PRD` was configured for Chart of Accounts `BKMG` with P&L account `5010032`.

### Default CO Assignment — `OKB9`

`KI235` identified the need for a CO-relevant account assignment for primary Cost Element `5010032`. `OKB9` was configured to assign Cost Center `CC9000` as the default receiver in the documented context.

### Actual Settlement — `KO88`

The actual settlement update run was completed for Period `09/2026`.

### Order Balance — `KKBC_ORD`

The resulting balance was:

| Category | Amount (EUR) |
|---|---:|
| Actual Debit Costs | `6,000.00` |
| Actual Delivery Credit | `0.00` |
| Settlement Offset | `-6,000.00` |
| Remaining Order Balance | **`0.00`** |

### FI Verification — `FB03`

FI document `1000000001` was verified:

- Document Type: `SA`
- Posting Date: `30.09.2026`
- Cost Center assignment: `CC9000`
- Production Order receiver: `1000020`
- Net balance: `€0.00`

Detailed case: [`03-business-processes/plan-to-produce/period-end-controlling-close.md`](../../03-business-processes/plan-to-produce/period-end-controlling-close.md)

## 7. Remaining CO Scope

The following areas remain future scope:

- Cost center master-data expansion
- Internal allocations
- Planning and budgeting
- Management-accounting reporting
- Broader R2R period-end activities and financial reporting

## Status

**Status: Manufacturing CO-PC period-end close completed; broader CO and R2R scope remains open.**
