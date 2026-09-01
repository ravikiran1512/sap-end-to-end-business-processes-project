# Procure-to-Pay (P2P) — End-to-End Lifecycle

## Executive Summary

The TechNova procurement scenario is now documented through the complete **Procure-to-Pay (P2P)** lifecycle for Company Code `9000`, from purchase order creation through goods receipt, invoice verification, FI posting, outgoing vendor payment, and final settlement.

The case demonstrates logistics execution, 3-way matching, tax handling, FI/MM integration, document-number configuration, G/L master-data correction, Universal Journal verification, and vendor open-item clearing.

## Business Context

| Object | Value |
|---|---|
| Company Code | `9000` — TechNova Mfg. GmbH |
| Controlling Area | `9000` |
| Fiscal Year / Period | `2026 / 08` |
| Vendor | `12026` — Apex Industrial Supplies |
| Purchase Order | `4500000149` |
| Material | TechNova 15.6" Display Panel |
| Quantity | `10 EA` |
| Net Value | `€500.00` |
| Input VAT | `€95.00` |
| Gross Payable | `€595.00` |

## End-to-End Document Flow

```text
ME21N — Purchase Order 4500000149
        ↓
MIGO — Goods Receipt, Movement 101
        ↓
Material Document 5000000062
        ↓
MIRO — Logistics Invoice Verification
        ↓
Invoice 5105600101
        ↓
FI Document 5100000000
        ↓
Vendor Open Item €595.00
        ↓
F-53 — Manual Outgoing Payment
        ↓
Payment Document 5000000000
        ↓
Vendor Liability Cleared
```

## 1. Purchase Order — `ME21N`

Purchase Order `4500000149` was created for Vendor `12026` — Apex Industrial Supplies.

- Material: TechNova 15.6" Display Panel
- Quantity: `10 EA`
- Unit Price: `€50.00`
- Net PO Value: `€500.00`

## 2. Goods Receipt — `MIGO`

The purchase order was received using:

- Business Operation: `A01 Goods Receipt`
- Reference: `R01 Purchase Order`
- Movement Type: `101`
- Material Document: `5000000062`

### Financial Impact

- Inventory / stock: **Debit €500.00**
- GR/IR Clearing `2010621`: **Credit €500.00**

This established the GR/IR interim position for invoice verification.

## 3. Logistics Invoice Verification — `MIRO`

### Number Range Resolution

The first invoice attempt failed because number range `51` was missing for Company Code `9000`, fiscal year `2026`.

`FBN1 / OMRJ` was used to create:

```text
Interval 51
From: 5100000000
To:   5199999999
Year: 2026
```

### Posting Period Alignment

The active MM posting period was `08/2026`. The invoice posting date was aligned to `31.08.2026`, after which the PO line populated successfully.

### 3-Way Match

The invoice matched the purchase order and goods receipt:

- Ordered: `10 EA`
- Received: `10 EA`
- Invoiced: `10 EA`
- Net: `€500.00`

### Tax

Tax Code `A1` — 19% German domestic VAT was applied:

- Net amount: `€500.00`
- Input VAT: `€95.00`
- Gross payable: `€595.00`
- MIRO balance: `€0.00`

### G/L Master-Data Corrections — `FS00`

Invoice simulation exposed tax-control restrictions on:

- Expense account `5010032`
- GR/IR clearing account `2010621`

Their Tax Category settings were updated to `*` to allow the required postings according to the executed scenario.

### Posted Documents

- Logistics invoice: `5105600101`
- Follow-on FI document: `5100000000`

### Invoice Accounting

| Account | Debit | Credit |
|---|---:|---:|
| GR/IR Clearing `2010621` | €500.00 | — |
| Input Tax `2300000` | €95.00 | — |
| Vendor `12026` | — | €595.00 |

The invoice clears the GR/IR interim liability and creates the vendor payable.

## 4. FI Verification — `MIR4`

The follow-on accounting document `5100000000` was reviewed through the invoice document / accounting view.

The financial posting confirmed:

- GR/IR clearing reversal of `€500.00`
- Input-tax debit of `€95.00`
- Vendor credit of `€595.00`

## 5. Vendor Payment — `F-53`

The vendor liability was settled manually from Bank Account `110000`.

### Number Range Resolution

Document Type `KZ` required number range interval `05` for fiscal year `2026`.

The final interval was created in `FBN1` as:

```text
Interval 05
From: 0500000000
To:   0599999999
Year: 2026
```

The configuration avoided overlap with the existing standard interval `01`.

### Payment Processing

The vendor open item of `€595.00` was selected and fully assigned, resulting in a balance of `€0.00`.

- Payment Document: `5000000000`
- Vendor: `12026`
- Bank Account: `110000`
- Amount: `€595.00`

### Payment Accounting

| Account | Debit | Credit |
|---|---:|---:|
| Vendor `12026` | €595.00 | — |
| Bank `110000` | — | €595.00 |

## Final Reconciliation

| Account | Debit | Credit | Net Effect |
|---|---:|---:|---:|
| Inventory / Stock | €500.00 | — | +€500.00 |
| GR/IR `2010621` | €500.00 | €500.00 | €0.00 |
| Input Tax `2300000` | €95.00 | — | +€95.00 |
| Vendor `12026` | €595.00 | €595.00 | €0.00 |
| Bank `110000` | — | €595.00 | -€595.00 |

## Final Status

**P2P lifecycle completed and financially settled.**

The purchase order was received, invoiced, posted to FI, and paid. GR/IR is cleared, the vendor liability is settled, and the documented vendor open item has a zero remaining balance.

## Related Documentation

- [MM-FI P2P Integration](../../06-integration/mm-fi-p2p-settlement.md)
- [Configuration Register](../../04-configuration/README.md)
- [Testing & Validation](../../07-testing/README.md)
- [Evidence](../../08-evidence/README.md)
