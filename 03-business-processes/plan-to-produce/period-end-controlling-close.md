# Period-End Controlling Close — Production Order `1000020`

## Executive Summary

This case documents the period-end Controlling close for Production Order `1000020` in SAP S/4HANA. The execution covers variance assessment, settlement-document number-range resolution, automatic account determination, default CO account assignment, actual settlement, order-balance verification, and FI journal-entry inspection.

The close was executed for Material `194 — TechNova Business Laptop` in Plant `TN01`, Controlling Area `9000`, for Period `09/2026` with posting date `30.09.2026`.

## 1. Master Data & Organizational Context

| Parameter | Value | Description |
|---|---|---|
| Controlling Area | `9000` | TechNova Mfg. GmbH |
| Plant | `TN01` | TechNova Manufacturing Plant |
| Production Order | `1000020` | Standard production order |
| Order Type | `PP01` | Standard Production Order |
| Material | `194` | TechNova Business Laptop (`FERT`) |
| Storage Location | `FG10` | Finished Goods Location |
| Chart of Accounts | `BKMG` | Multi-GAAP Group Chart of Accounts |
| Settled Variance Account | `5010032` | Primary cost element / variance offset |
| Default Cost Center | `CC9000` | Production overhead / factory cost center |
| Closed Period / Fiscal Year | `09/2026` | Posting date `30.09.2026` |

## 2. Variance Assessment — `KKS2`

During variance calculation for Period `09/2026`, the system returned:

```text
KV 017: No orders (order items) could be processed
```

The documented diagnosis was that the order header did not have the required variance-key / target-cost setup for the intended `KKS2` processing. For this production-order scenario, the close proceeded through the order's settlement path using `TECO` / `SETC` and `KO88` rather than treating `KKS2` target-cost splits as a prerequisite.

## 3. Settlement Number Range — `CO_ABRECHN`

The first `KO88` update attempt returned:

```text
KD522: Define a number range for settlement documents in controlling area 9000
```

### Root Cause

Interval `01` existed in settlement number-range object `CO_ABRECHN`, but Controlling Area `9000` was listed under **Non-Assigned Elements** instead of being assigned to the active group.

### Resolution

1. Opened Group Maintenance using `Goto → Groups → Change`.
2. Selected Controlling Area `9000`.
3. Assigned it to the active number-range group containing interval `01`.
4. Confirmed the interval range `0100000000–0199999999`.

## 4. Automatic Account Determination — `OBYC / PRD`

The subsequent `KO88` execution returned:

```text
M8147: Account determination for entry BKMG PRD not possible
```

### Root Cause

The settlement posting required a Price Difference (`PRD`) account in MM-FI automatic account determination for Chart of Accounts `BKMG`.

### Resolution

Configured `OBYC → PRD` for Chart of Accounts `BKMG` and assigned P&L account `5010032` for the documented price-difference determination.

## 5. Default CO Account Assignment — `OKB9`

Post-validation returned:

```text
KI235: Account 5010032 requires an account assignment relevant to cost accounting
```

### Root Cause

G/L `5010032` was configured as a Primary Cost Element (Category `1`) and therefore required a valid CO receiver during the relevant posting.

### Resolution

Configured `OKB9` with the following default assignment:

```text
Company Code / CO context    9000
Cost Element                 5010032
Default Cost Center          CC9000
```

## 6. Actual Settlement — `KO88`

After the number-range, account-determination, and CO account-assignment corrections, the actual settlement update run was executed for Period `09/2026`.

The production-order balance was fully liquidated through settlement.

## 7. Order Balance Verification — `KKBC_ORD`

| Category | Amount (EUR) | Status |
|---|---:|---|
| Actual Debit Costs — Components & Routing | `6,000.00` | Incurred |
| Actual Delivery Credit — GR 101 / MIGO | `0.00` | No standard receipt valuation credit |
| Settlement Offset — `KO88` Update Run | `-6,000.00` | Cleared to FI/CO |
| Remaining Order Balance | **`0.00`** | **Fully Balanced** |

The `KKBC_ORD` result confirms that the production order no longer carries the documented unsettled balance.

## 8. Financial Accounting Verification — `FB03`

The settlement generated FI document `1000000001`:

- Document Type: `SA`
- Posting Date: `30.09.2026`
- Company Code: `9000`

```text
Item | PK | Account | Description          | Amount (EUR) | CO Assignment
-----|----|---------|----------------------|--------------|----------------------
001  | 81 | 5010032 | Funding: Expenses    |    6,000.00 | Cost Center CC9000
002  | 93 | 5010032 | Funding: Expenses    |   -6,000.00 | Production Order 1000020
-----|----|---------|----------------------|--------------|----------------------
Net Balance: 0.00 EUR
```

The FI document provides the financial posting trace for the settlement and shows the offset between the cost-center assignment and the production-order receiver.

## 9. Close Status

**Status: COMPLETED — Period-end Controlling close for Production Order `1000020` documented through settlement and FI verification.**

The earlier manufacturing execution milestone (`OPK4 → CO15 → MIGO → MMBE → CO03`) is therefore extended by the period-end close sequence documented here:

```text
Production Execution
        ↓
CO02 / TECO + SETC
        ↓
KKS2 — Variance Assessment
        ↓
KO88 — Actual Settlement
        ↓
KKBC_ORD — Order Balance = €0.00
        ↓
FB03 — FI Document 1000000001
        ↓
Manufacturing Period-End Close
```

## 10. Evidence Placeholders

The supplied documentation specifies the following screenshot evidence sequence. Add the corresponding SAP GUI captures to `08-evidence/screenshots/plan-to-produce/` when available:

```text
01_co_abrechn_group_assignment.png
02_obyc_prd_account_5010032.png
03_okb9_default_assignment.png
04_ko88_actual_settlement_update.png
05_kkbc_ord_zero_balance.png
06_fb03_settlement_document_1000000001.png
```

## Related Documentation

- [Plan-to-Produce Execution Case](README.md)
- [CO Documentation](../../docs/co/README.md)
- [Testing & Validation](../../07-testing/README.md)
- [Evidence](../../08-evidence/README.md)
