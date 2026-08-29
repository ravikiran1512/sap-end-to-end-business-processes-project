# Material Master — 194 — TechNova Business Laptop

## Implementation Overview

Material **194 — TechNova Business Laptop** is the current material master used in the TechNova SAP S/4HANA end-to-end project. The material is maintained as a finished product so the same master-data object can support sales, procurement, inventory, planning, logistics, and accounting integration.

> **Master-data revision:** The previous project material identifier **184** has been retired from the active project documentation. The current identifier is **194**.

## 1. Material Master Profile

| Field | Current value |
|---|---|
| Material | `194` |
| Description | `TechNova Business Laptop` |
| Material Type | Finished Product |
| Industry | Mechanical engineering |
| Base Unit | `EA – Each` |
| Gross Weight | `2 KG` |
| Net Weight | `1.700 KG` |
| Dimensions | `35 × 24 × 2 cm` |
| Plant | `0001 – AN PLANT – BENGALURU` |
| Sales Organization | `0001 – Sales Org. 001` |
| Distribution Channel | `01 – Distribution Channel 01` |
| Classification | Class Type `001` / Class `1000` |
| Tax Classification | `1 – Full tax` |
| Availability Check | `02 – Individual requirements` |
| Profit Center | `PC0001` |
| Inventory Planning Mode | `eSPP calculation` |

## 2. Shipping-Relevant Data

| Attribute | Value |
|---|---|
| Loading Group | `0002 – Forklift` |
| Transportation Group | `0004 – Parcel` |

These attributes participate in the shipping-point determination used by the SD execution.

## 3. Sales Execution Dependency

```text
Material Master 194
       ↓
MM03 Verification
       ↓
MM02 Shipping Data
       ↓
Shipping Point Determination
       ↓
VA01 Sales Order 12
       ↓
VL01N Outbound Delivery
       ↓
Picking
       ↓
Post Goods Issue
       ↓
Billing
       ↓
FI / Accounts Receivable
```

## 4. Traceability

- The active project material identifier is **194**.
- The documented master-data attributes are carried forward from the previously recorded laptop material implementation because the requested revision changes the material identifier.
- Exact Material Group coding is not stated where the earlier evidence did not preserve the selected code.
- Practice-system values such as Plant `0001` remain explicitly identified as executed environment values.

## 5. Integration Value

Material 194 is a shared master-data object across the end-to-end model:

- **MM:** material master, procurement, inventory, and planning
- **SD:** sales order, shipping, delivery, and billing
- **FI:** revenue, tax, receivables, and accounting document integration
- **CO:** profit-center and management-accounting relevance
- **PP:** future production and material-requirement scenarios

## 6. Current Status

**Status: Active project material — 194**

The project now uses Material **194** as the current TechNova Business Laptop identifier. The next O2C execution milestone remains outbound delivery creation with `VL01N` using Sales Order `12`.
