# TechNova SAP Implementation Evidence

This section contains SAP GUI evidence captured during the **TechNova SAP End-to-End Implementation**.

## Evidence Index

| Evidence | SAP Area | Description |
|---|---|---|
| Company Code Overview | Enterprise Structure / FI | Company Code `9000` configuration overview |
| Company Code Global Data | Enterprise Structure / FI | Core organizational and accounting parameters |
| G/L Account — Receivables | FI / G/L Master Data | G/L account `1020131` master-data configuration |
| Save Warning Validation | FI / G/L Master Data | SAP validation behavior during account creation |
| Material 194 — Material Master | MM / Material Master | Material `194 — TechNova Business Laptop` creation and validation |
| Material 194 — MM03 Verification | MM / Material Master | Post-creation verification of stored material data |
| Material 194 — Shipping Data | MM / Logistics | Loading Group `0002 — Forklift` and Transportation Group `0004 — Parcel` |
| Shipping Point Determination | SD / Logistics Execution | Shipping Condition `01` + Loading Group `0002` + Plant `0001` → Shipping Point `0001` in the executed practice scenario |
| Sales Order 12 | SD / O2C | Standard Order for customer `1000000020`, material `194`, quantity `10 EA` |
| Sales Order Pricing | SD / Pricing | PR00 price `1.00 EUR / EA`; final net value `10.00 EUR` |
| Sales Order Save Confirmation | SD / O2C | SAP confirmation that Standard Order `12` was saved |

## Current Evidence Pack — 24 August 2026

The milestone extends the completed Material Master creation into the first Order-to-Cash execution:

**MM03 verification → MM02 shipping data → Shipping Point Determination → VA01 Sales Order 12**.

Detailed document: [`docs/sd/material-verification-to-sales-order-12.md`](../docs/sd/material-verification-to-sales-order-12.md)

PDF evidence pack: `evidence/implementation-evidence-packs/SAP_Material_Verification_to_Sales_Order_12.pdf`

## Evidence Organization

Screenshots are organized by SAP area under `evidence/screenshots/`. MM verification and shipping evidence is maintained under `mm/`; shipping-point and sales-order evidence is maintained under `sd/`; the billing-resolution sequence is maintained under `sd/billing-resolution/`.

## Environment and Traceability

The evidence records actual values visible in the available SAP practice/server environment. Values such as Plant `0001`, Shipping Point `0001`, and customer `1000000020` are retained as execution evidence and are not silently converted into the confirmed TechNova enterprise IDs from the project master plan.

## Security

The source project material does not intentionally include passwords, connection strings, or server-access credentials. Screenshots should be reviewed before public publication to ensure that confidential tenant or system information is not exposed.

## Evidence Principle

The repository documents the executed SAP state without inventing values that are not preserved by the evidence. This rule applies to both configuration and business-process execution.
