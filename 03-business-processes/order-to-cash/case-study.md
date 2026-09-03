# SAP S/4HANA Order-to-Cash (O2C) End-to-End Execution Case Study

## Executive Summary

This case study documents the completed Order-to-Cash lifecycle for **TechNova Manufacturing GmbH**, Company Code `9000`, using the core project material **`194 — TechNova Laptop`** and customer **`1000000029 — Delta Electronics`**.

The process was executed from Sales Order through outbound delivery, picking, Post Goods Issue, billing, automatic SD-FI posting, incoming customer payment, and final Accounts Receivable clearing.

## Business Context

| Object | Value |
|---|---|
| Company Code | `9000` |
| Chart of Accounts | `BKMG` |
| Customer | `1000000029 — Delta Electronics` |
| Material | `194 — TechNova Laptop` |
| Quantity | `10 EA` |
| Unit Price | `€850.00` |
| Net Value | `€8,500.00` |
| Output VAT | `€1,615.00` |
| Gross Settlement | `€10,115.00` |

## End-to-End Execution

### 1. Sales Order — `VA01`

- Sales Order: `18`
- Quantity: `10 EA`
- Net Value: `€8,500.00`
- VAT: `€1,615.00`
- Gross Value: `€10,115.00`

### 2. Outbound Delivery & Picking — `VL01N`

- Delivery: `80000029`
- Shipping Point: `TN01`
- Storage Location: `FG10`
- Picked Quantity: `10 EA`

### 3. Post Goods Issue — `VL02N`

- Movement Type: `601`
- Material Document: `4900000105`

The PGI reduced finished-goods inventory and triggered the COGS/inventory accounting interface.

## PGI Troubleshooting

### MM Posting Period — `MMPV`

PGI was initially blocked by error `M7 053` because the Materials Management posting period had not been rolled forward to September 2026.

Resolution:

`MMPV → close 08/2026 → open 09/2026 → Company Code 9000`

### Automatic Account Determination — `OBYC`

After the period issue was resolved, error `M8 147` identified a missing account-determination entry:

`BKMG / GBB / 0001 / VAX / 7920`

The COGS assignment was maintained using G/L `6010531`.

Result: PGI posted successfully and Material Document `4900000105` was generated.

## Billing & FI Integration

### 4. Billing — `VF01`

- Billing Document: `90000037`
- Net Value: `€8,500.00`
- Output VAT: `€1,615.00`
- Gross Value: `€10,115.00`

### 5. FI Journal Entry

Automatic SD-FI integration generated Journal Entry `9000000001`.

| Account | Debit | Credit |
|---|---:|---:|
| Customer `1000000029` | €10,115.00 | — |
| Revenue `6010131` | — | €8,500.00 |
| Output VAT `2300000` | — | €1,615.00 |

**Debit = Credit = €10,115.00**

## Incoming Payment & Clearing

### 6. Incoming Payment — `F-28`

- Payment Document: `1000000000`
- Bank Account: `110000`
- Amount: `€10,115.00`
- Customer: `1000000029`
- Unassigned Difference: `€0.00`

Accounting effect:

- Debit Bank `110000`: `€10,115.00`
- Credit Customer `1000000029`: `€10,115.00`

### 7. Final AR Verification — `FBL5N`

The invoice and payment were fully cleared.

- Open Items: `0`
- Final Customer Balance: **`€0.00`**

## Final Document Flow

```text
VA01 Order 18
   ↓
VL01N Delivery 80000029
   ↓
VL02N PGI / Material Document 4900000105
   ↓
VF01 Billing 90000037
   ↓
SD-FI Journal Entry 9000000001
   ↓
F-28 Payment 1000000000
   ↓
FBL5N Customer Balance €0.00
```

## Implementation Significance

This execution demonstrates a complete O2C lifecycle together with practical integration troubleshooting. The scenario proves capability across SD logistics, MM period control, MM-FI automatic account determination, FI-AR posting, customer payment processing, and final reconciliation.

## Evidence

- Evidence pack: [`../../08-evidence/evidence-packs/SAP_O2C_Execution_Report.md`](../../08-evidence/evidence-packs/SAP_O2C_Execution_Report.md)
- Screenshot location: `../../08-evidence/screenshots/o2c/`

The supplied execution report contains 9 pages and 14 documented figures, while the accompanying screenshot package contains 18 high-resolution SAP captures.

## Historical Note

The repository also preserves an earlier separate SD-FI billing-resolution case involving Customer `1000000021`, Billing `90000032`, and Material `10194`. That case remains useful as a troubleshooting reference but is no longer the current core O2C execution.

## Status

**PASS — complete O2C lifecycle executed, financially posted, paid, and cleared.**