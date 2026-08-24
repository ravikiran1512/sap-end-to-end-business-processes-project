# Order-to-Cash (O2C)

I am building the Order-to-Cash process as an integrated business-process chain rather than as isolated SD transactions.

## Current Evidence Milestone

**Completed:** Material verification → shipping-relevant material data → shipping-point determination → **Sales Order 12**.

I verified Material `184`, maintained Loading Group `0002` and Transportation Group `0004`, corrected the shipping-point determination combination required by the executed practice scenario, and created Standard Sales Order `12` for customer `1000000020` with 10 EA of Material `184`.

```text
Material 184
   ↓
MM03 verification                 ✓
   ↓
MM02 shipping data               ✓
   ↓
Shipping Point Determination     ✓
   ↓
VA01 Sales Order 12              ✓
   ↓
VL01N Outbound Delivery          ← NEXT
   ↓
Picking
   ↓
Post Goods Issue (PGI)
   ↓
Billing
   ↓
FI / Accounts Receivable Impact
```

## Sales Order 12 Result

| Field | Executed value |
|---|---|
| Sales Order | `12` |
| Customer | `1000000020 — TechNova GmbH` |
| Customer Reference | `TECHNOVA-001` |
| Material | `184 — TechNova Business Laptop` |
| Quantity | `10 EA` |
| Pricing Condition | `PR00 — Price` |
| Price | `1.00 EUR / EA` |
| Net Value | `10.00 EUR` |
| Delivering Plant | `0001 — AN PLANT – BENGALURU` |
| Shipping Point | `0001` |

## What I Learned From This Milestone

I demonstrated that the sales order depends on master data and configuration maintained earlier. I used the material master to provide product and logistics attributes, used the loading group in shipping-point determination, connected the sales item to the delivering plant, and maintained PR00 pricing to resolve the order incompletion.

## Next Step

I will continue with:

**`VL01N` — Create Outbound Delivery with reference to Sales Order `12`.**

After that I will execute and document picking, Post Goods Issue, billing, and the resulting FI/Accounts Receivable integration.

## Detailed Evidence

[`docs/sd/material-verification-to-sales-order-12.md`](../../docs/sd/material-verification-to-sales-order-12.md)

Screenshot mapping: [`evidence/screenshots/SCREENSHOT-MANIFEST.md`](../../evidence/screenshots/SCREENSHOT-MANIFEST.md)

## Environment Note

The executed screenshots contain practice/server values such as Plant `0001`, Shipping Point `0001`, and customer `1000000020`. I record these as actual execution evidence and do not silently reclassify them as confirmed TechNova enterprise IDs.
