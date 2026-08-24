# Order-to-Cash

End-to-end sales flow covering customer demand, sales order, outbound delivery, picking, goods issue, billing, and accounting integration.

## Current Evidence Milestone

**Completed:** Material verification → shipping data → shipping-point determination → **Sales Order 12**.

```text
Material 184
   ↓
MM03 verification
   ↓
MM02 shipping data
   ↓
Shipping Point Determination
   ↓
VA01 Sales Order 12
   ↓
VL01N Outbound Delivery  ← next
   ↓
Picking
   ↓
PGI
   ↓
Billing
   ↓
FI / AR integration
```

Detailed execution evidence: [`docs/sd/material-verification-to-sales-order-12.md`](../../docs/sd/material-verification-to-sales-order-12.md).