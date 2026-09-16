# Plan-to-Produce (Manufacturing) — Completed End-to-End Execution & Period-End Close

## Executive Summary

The Plan-to-Produce manufacturing workflow for **TechNova Manufacturing GmbH** has been executed and validated in SAP S/4HANA using Production Order `1000020` for Material `194 — TechNova Business Laptop`.

The completed case now covers production confirmation, finished-goods receipt, inventory reconciliation, production-order validation, manufacturing configuration troubleshooting, period-end Controlling processing, order settlement, and FI verification.

## Organizational & Master Data Scope

| Parameter | Value | Business Context |
|---|---|---|
| Company Code | `9000` | TechNova Mfg. GmbH |
| Controlling Area | `9000` | Standard controlling area |
| Plant | `TN01` | TechNova Manufacturing Plant |
| Storage Location | `FG10` | Finished Goods Warehouse |
| Production Order | `1000020` | Manufacturing execution order |
| Order Type | `PP01` | Standard Production Order |
| Material | `194` | TechNova Business Laptop (`FERT`) |
| Chart of Accounts | `BKMG` | Multi-GAAP chart |
| Valuation Class | `7920` | Finished Products |
| Settled / Offset Account | `5010032` | Primary cost element / variance offset |
| Default Cost Center | `CC9000` | Production overhead / factory cost center |
| Close Period | `09/2026` | Posting Date `30.09.2026` |

## End-to-End Manufacturing Flow

```text
Production Order 1000020
        ↓
OPK4 — Confirmation Parameters
        ↓
CO15 — Confirm 10 EA Yield
        ↓
MIGO — Goods Receipt / Movement 101
        ↓
Material Document 5000000063
        ↓
MMBE — 95 EA Unrestricted Stock
        ↓
CO03 — Production Order Validation
        ↓
CO02 / TECO + SETC
        ↓
KKS2 — Variance Assessment
        ↓
CO_ABRECHN — Settlement Number Range
        ↓
OBYC / PRD — Account Determination
        ↓
OKB9 — Default CO Assignment
        ↓
KO88 — Actual Settlement
        ↓
KKBC_ORD — Order Balance €0.00
        ↓
FB03 — FI Document 1000000001
```

## Phase 1 — Production Execution

### Confirmation Configuration (`OPK4`)

Confirmation parameters were maintained for Plant `TN01` and Order Type `PP01` for the documented production scenario.

### Production Confirmation (`CO15`)

Production Order `1000020` was confirmed with a yield of `10 EA`. The production confirmation established the actual output quantity and progressed the production order through the documented operational statuses.

### Goods Receipt (`MIGO`)

Finished-goods receipt was posted using Movement Type `101`:

- Production Order: `1000020`
- Material: `194`
- Quantity: `10 EA`
- Plant: `TN01`
- Storage Location: `FG10`
- Material Document: `5000000063`

### Inventory & Order Validation

`MMBE` confirmed `95 EA` unrestricted stock in `FG10`. `CO03` confirmed `10 EA` total confirmed quantity and `10 EA` delivered quantity, with the documented final operational status including `REL`, `CNF`, and `PDLV`.

## Phase 2 — Manufacturing Configuration & Troubleshooting

The production execution required resolution of the following configuration issues:

1. `OBYC` GBB-AUF account determination for `BKMG / GBB / 0001 / AUF / 7920`.
2. `KI280` cost-element compatibility, resulting in use of G/L `5010032` for the documented production-order posting.
3. `OPK9` valuation configuration, assigning Valuation Area `TN01` to Valuation Variant `001`.

After correction and validation, the MIGO document check returned **Document is O.K.** and the goods receipt posted successfully.

## Phase 3 — Period-End Controlling Close (CO-PC)

The production order was subsequently processed for the documented Period `09/2026` close.

### Variance Assessment (`KKS2`)

The initial variance calculation returned:

```text
KV 017: No orders (order items) could be processed
```

The documented resolution was to continue through the production-order settlement path using `TECO` / `SETC` and `KO88` rather than treating target-cost version splits as a prerequisite for this scenario.

### Settlement Number Range (`CO_ABRECHN`)

`KO88` initially returned `KD522`, requiring a settlement-document number range for Controlling Area `9000`.

Controlling Area `9000` was assigned to the active settlement number-range group containing interval `01` (`0100000000–0199999999`).

### Price Difference Account Determination (`OBYC / PRD`)

The subsequent settlement attempt returned `M8147` for missing `BKMG PRD` account determination. `OBYC → PRD` was configured for Chart of Accounts `BKMG` with P&L account `5010032`.

### Default CO Assignment (`OKB9`)

`KI235` identified the need for a cost-accounting assignment for G/L `5010032`. `OKB9` was configured to assign Company Code / CO context `9000` and Cost Element `5010032` to default Cost Center `CC9000`.

### Actual Settlement (`KO88`)

After the documented corrections, the actual settlement update run was executed for Period `09/2026`.

## Phase 4 — Financial Reconciliation

### Order Balance (`KKBC_ORD`)

| Category | Amount (EUR) | Status |
|---|---:|---|
| Actual Debit Costs | `6,000.00` | Incurred |
| Actual Delivery Credit | `0.00` | No standard receipt valuation credit |
| Settlement Offset | `-6,000.00` | Cleared to FI/CO |
| Remaining Order Balance | **`0.00`** | **Fully Balanced** |

### FI Journal Entry (`FB03`)

The settlement generated FI document `1000000001`:

- Document Type: `SA`
- Posting Date: `30.09.2026`
- Settlement account: `5010032`
- Cost Center assignment: `CC9000`
- Production Order receiver: `1000020`

```text
Item | PK | Account | Description          | Amount (EUR) | CO Assignment
-----|----|---------|----------------------|--------------|----------------------
001  | 81 | 5010032 | Funding: Expenses    |    6,000.00 | Cost Center CC9000
002  | 93 | 5010032 | Funding: Expenses    |   -6,000.00 | Production Order 1000020
-----|----|---------|----------------------|--------------|----------------------
Net Balance: 0.00 EUR
```

## Final Result

**Status: COMPLETED — Production execution, confirmation, finished-goods receipt, inventory reconciliation, period-end Controlling settlement, order-balance verification, and FI posting verification completed.**

The manufacturing case is now complete through the documented CO-PC period-end close. Broader Record-to-Report activities, allocations, reporting, and other financial-close scenarios remain separate future scope.

## Evidence

- [Period-End Controlling Close](period-end-controlling-close.md)
- [Plan-to-Produce Evidence Pack](../../08-evidence/evidence-packs/SAP_Plan_to_Produce_Execution_Report.md)
- Screenshot location: `../../08-evidence/screenshots/plan-to-produce/`
