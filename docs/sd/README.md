# Sales and Distribution (SD)

## Current SD Execution

**Status: In Progress — Core Sales Order milestone completed; separate SD-FI-AR billing case documented through customer clearing.**

The active core O2C material is **194 — TechNova Business Laptop**. The first executed sales milestone is Standard Sales Order **12**.

## Executed Core Milestone — 24 August 2026

- `MM03` — verified Material `194`.
- `MM02` — maintained Loading Group `0002 — Forklift`.
- `MM02` — maintained Transportation Group `0004 — Parcel`.
- Shipping Point Determination — Shipping Condition `01` + Loading Group `0002` + Plant `0001` → Shipping Point `0001`.
- `VA01` — created Standard Sales Order `12`.
- Customer — `1000000020 — TechNova GmbH`.
- Customer Reference — `TECHNOVA-001`.
- Material — `194 — TechNova Business Laptop`.
- Quantity — `10 EA`.
- Pricing — `PR00`, `1.00 EUR / EA`.
- Net Value — `10.00 EUR`.

Detailed core execution: [`material-verification-to-sales-order-12.md`](material-verification-to-sales-order-12.md)

## Completed SD-FI-AR Billing Case

The project also contains a separate supplied billing-release and customer-accounting case covering:

**VF02 → VKOA → OB40 → FS00 → FBN1/OBA7 → OBA3 → VF02 → FB03 → FBL5N → F-28 → FBL5N**

Key documented result:

- Billing document: `90000032` / F2
- FI document: `9000000000` / RV
- Customer receivable: `€5,950.00`
- Incoming payment: `6000000000` / `€5,950.00`
- Final customer balance: **`€0.00`**

Detailed integration case study: [`../integration/sd-fi-billing-resolution.md`](../integration/sd-fi-billing-resolution.md)

## End-to-End SD Flow — Core Project

**Customer Requirement → Sales Order → Outbound Delivery → Picking → Post Goods Issue → Billing → Financial Posting**

## Next Core Execution Step

`VL01N` — Create Outbound Delivery with reference to Sales Order `12`.

This next step applies to the **core Material 194 / Sales Order 12 execution chain**. It is not a status indicator for the separate supplied billing case, which is already documented through customer clearing.

## Environment Note

The executed core O2C milestone contains practice/server values such as Plant `0001`, Shipping Point `0001`, and customer `1000000020`. These are retained as execution evidence and are not silently reclassified as confirmed TechNova enterprise IDs.

The separate billing case records customer `1000000021` and material `10194`; those source values remain preserved in their case-study context.

## Portfolio Focus

The SD documentation emphasizes document flow, master-data dependencies, configuration troubleshooting, billing-to-FI integration, customer accounting, and evidence-driven implementation rather than isolated transaction steps.
