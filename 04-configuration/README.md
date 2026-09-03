# 04 — Configuration

Centralized technical configuration reference for the implementation.

## Domains

- **FI** — Company Code, G/L, tax, document numbering, customer/vendor accounting
- **CO** — Controlling Area, CO Version-to-Ledger alignment, Universal Journal prerequisites
- **MM** — material/logistics dependencies, procurement, goods receipt, invoice verification, period control
- **SD** — shipping-point determination, revenue determination, billing integration

## Current Configuration Milestones

### CO / Universal Journal

`CO Area 9000 + Version 0 → Ledger 0L`

`PRJ_9000 / B2K → 0 errors / 0 warnings`

### Core O2C — Completed

The completed core O2C execution required two configuration corrections during PGI:

| Area | Transaction | Issue | Resolution |
|---|---|---|---|
| MM posting period | `MMPV` | Error `M7 053`: period `09/2026` not open | Closed `08/2026` and opened `09/2026` for Company Code `9000` |
| Automatic account determination | `OBYC` | Error `M8 147`: missing `BKMG / GBB / 0001 / VAX / 7920` | Assigned COGS G/L `6010531` |

Core O2C document chain:

`Order 18 → Delivery 80000029 → Material Document 4900000105 → Billing 90000037 → FI 9000000001 → F-28 1000000000 → Customer balance €0.00`

### SD-FI Historical Billing Resolution

`VKOA → OB40 → FS00 → FBN1/OBA7 → VF02 → FB03`

The earlier billing-resolution case remains preserved as a separate troubleshooting reference.

### Procure-to-Pay — Completed

The completed P2P lifecycle required the following technical configuration and master-data corrections:

| Area | Transaction / Object | Configuration |
|---|---|---|
| MIRO document numbering | `FBN1 / OMRJ` | Interval `51`, Year `2026`, `5100000000–5199999999` |
| MM posting period | MIRO | Active period `08/2026`; posting date aligned to `31.08.2026` |
| Expense G/L tax control | `FS00` / `5010032` | Tax Category updated to `*` |
| GR/IR tax control | `FS00` / `2010621` | Tax Category updated to `*` |
| Input tax | Tax Code `A1` | 19% VAT; `€95.00` on `€500.00` net |
| Vendor payment numbering | `FBN1` / Document Type `KZ` | Interval `05`, Year `2026`, `0500000000–0599999999` |
| Bank settlement | `F-53` | Bank `110000`, Vendor `12026`, `€595.00` |

### P2P Document Chain

`PO 4500000149 → MIGO 5000000062 → MIRO 5105600101 → FI 5100000000 → F-53 5000000000`

The final GR/IR and vendor payable positions are both cleared to zero.

Detailed integration case: [`../06-integration/mm-fi-p2p-settlement.md`](../06-integration/mm-fi-p2p-settlement.md)