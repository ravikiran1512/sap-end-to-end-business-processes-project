# Order-to-Cash (O2C)

## End-to-End Flow

`VA01 → VL01N → VL02N → VF01 → VF02 → FB03 → FBL5N → F-28 → FBL5N`

## Current State

- Core execution: Sales Order `12`; `VL01N` is next.
- Billing case: Billing `90000032` → FI `9000000000` → Payment `6000000000` → Customer balance `€0.00`.
- SD-FI diagnostic documentation is preserved under the integration section during the repository migration.

## Key Documents

- [SD-FI Integration Resolution](../../06-integration/sd-fi-billing-resolution.md)

The detailed O2C execution narrative is retained during restructuring; this page serves as the business-process navigation point.
