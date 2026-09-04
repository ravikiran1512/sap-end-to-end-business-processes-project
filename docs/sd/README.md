# Sales and Distribution (SD)

## Current SD Execution

**Status: Completed — Core O2C lifecycle executed through delivery, PGI, billing, FI posting, incoming payment, and customer clearing.**

The active core O2C material is **194 — TechNova Business Laptop**. The current completed execution is based on Sales Order **18**.

## Current Core O2C Milestone

- Material: `194 — TechNova Business Laptop`.
- Customer: `1000000029 — Delta Electronics`.
- Quantity: `10 EA`.
- Sales Order: `18`.
- Outbound Delivery: `80000029`.
- PGI Material Document: `4900000105`.
- Billing Document: `90000037`.
- FI Journal Entry: `9000000001`.
- Incoming Payment: `1000000000`.
- Final customer balance: `€0.00`.

The supplied execution package documents the logistics, billing, FI integration, payment settlement, and final reconciliation sequence.

## End-to-End SD Flow — Current Project

```text
VA01 — Sales Order 18
        ↓
VL01N — Outbound Delivery 80000029
        ↓
VL02N — Picking / Post Goods Issue
        ↓
Material Document 4900000105
        ↓
VF01 — Billing 90000037
        ↓
FI Journal Entry 9000000001
        ↓
F-28 — Incoming Payment 1000000000
        ↓
FBL5N — Customer Balance €0.00
```

## Current O2C Financial Result

| Position | Result |
|---|---:|
| Net Sales | `€8,500.00` |
| Output VAT | `€1,615.00` |
| Customer Receivable | `€10,115.00` |
| Incoming Payment | `€10,115.00` |
| Final Customer Balance | **`€0.00`** |

## Historical SD-FI-AR Billing Case

A separate supplied billing-release and customer-accounting case remains preserved as a historical troubleshooting reference. It covers:

**VF02 → VKOA → OB40 → FS00 → FBN1/OBA7 → OBA3 → VF02 → FB03 → FBL5N → F-28 → FBL5N**

Key documented result:

- Billing document: `90000032` / F2
- FI document: `9000000000` / RV
- Customer receivable: `€5,950.00`
- Incoming payment: `6000000000` / `€5,950.00`
- Final customer balance: **`€0.00`**

Detailed integration case study: [`../integration/sd-fi-billing-resolution.md`](../integration/sd-fi-billing-resolution.md)

## Historical Core Milestone — 24 August 2026

Sales Order `12` remains preserved in its original execution documentation as a historical milestone. It is not the current O2C status.

Detailed historical execution: [`material-verification-to-sales-order-12.md`](material-verification-to-sales-order-12.md)

## Evidence

Current O2C evidence is maintained under:

`08-evidence/screenshots/o2c/`

Evidence pack:

`08-evidence/evidence-packs/SAP_O2C_Execution_Report.md`

## Environment Note

Practice/server values are retained as execution evidence and are not silently reclassified as confirmed enterprise IDs. The separate historical billing case also preserves its source customer/material identifiers in its original case-study context.

## Portfolio Focus

The SD documentation emphasizes document flow, master-data dependencies, configuration troubleshooting, billing-to-FI integration, customer accounting, and evidence-driven implementation rather than isolated transaction steps.
