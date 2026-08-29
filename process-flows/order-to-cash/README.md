# Order-to-Cash (O2C)

The TechNova Order-to-Cash process is documented as an integrated business-process chain rather than as isolated SD transactions.

## Current Execution Milestone

**Completed:** Material 194 verification → shipping-relevant material data → shipping-point determination → **Sales Order 12**.

| Field | Executed value |
|---|---|
| Material | `194 — TechNova Business Laptop` |
| Sales Order | `12` |
| Customer | `1000000020 — TechNova GmbH` |
| Quantity | `10 EA` |
| PR00 | `1.00 EUR / EA` |
| Net Value | `10.00 EUR` |
| Plant | `0001` |
| Shipping Point | `0001` |

```text
Material 194
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

## SD-FI Billing Resolution Extension

A separate uploaded execution package has been integrated into the project under the SD/FI evidence area. It documents the diagnostic path from billing-account-determination errors through configuration and successful FI posting verification.

```text
Billing Document 90000032
        ↓
VF02 — Release to Accounting
        ↓
VKOA — Revenue Account Determination
        ↓
OB40 — Output Tax Account Determination
        ↓
FS00 — G/L Master Data Validation
        ↓
FBN1 — FI Document Number Range
        ↓
VF02 — Successful Release
        ↓
FB03 — Posted FI Document 9000000000
```

The uploaded billing evidence records material **10194**. Because the project master-data revision is **194**, the billing artifact preserves `10194` exactly as shown by the executed evidence rather than silently rewriting an evidence value that may represent a separate system object.

## Next O2C Step

**`VL01N` — Create Outbound Delivery with reference to Sales Order `12`.**

After delivery execution, the project will continue through picking, PGI, billing, and FI/AR validation.
