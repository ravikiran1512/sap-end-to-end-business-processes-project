# 04 — Configuration

Centralized technical configuration reference for the implementation.

## Domains

- **FI** — Company Code, G/L, tax, document numbering, customer accounting
- **CO** — Controlling Area, CO Version-to-Ledger alignment, Universal Journal prerequisites
- **MM** — material/logistics dependencies and procurement execution
- **SD** — shipping-point determination, revenue determination, billing integration

## Current Configuration Milestones

### CO / Universal Journal

`CO Area 9000 + Version 0 → Ledger 0L`

`PRJ_9000 / B2K → 0 errors / 0 warnings`

### SD-FI

`VKOA → OB40 → FS00 → FBN1/OBA7 → VF02 → FB03`

### MM

PO `4500000149` progressed to MIGO Goods Receipt, Movement Type `101`, Material Document `5000000062`.

Detailed legacy configuration records are being migrated here without loss of technical detail.
