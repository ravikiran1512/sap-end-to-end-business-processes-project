# 06 — Integration

Cross-module integration is documented here rather than duplicated inside each module.

## Active Integration Areas

### SD → FI
Billing `90000032` required revenue determination, tax account determination, G/L master data, FI number ranges, and customer-account prerequisites before generating FI document `9000000000`.

### CO → Universal Journal
CO Area `9000`, Version `0` was aligned to Leading Ledger `0L`; `PRJ_9000` / `B2K` completed the required journal-entry update activity.

### MM → FI
MIGO Goods Receipt for PO `4500000149` generated Material Document `5000000062` and established the GR/IR interim position for subsequent `MIRO` invoice verification.

## Detailed Resolution

- [SD-FI Billing Resolution](sd-fi-billing-resolution.md)
