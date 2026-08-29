# Materials Management (MM)

## Current MM Implementation

The active TechNova laptop material is **194 — TechNova Business Laptop**. The previous identifier has been retired from the active project documentation.

## Material 194 Profile

| Item | Value / Result |
|---|---|
| Material | `194` |
| Description | TechNova Business Laptop |
| Material Type | Finished Product |
| Industry | Mechanical engineering |
| Base Unit | EA – Each |
| Gross Weight | 2 KG |
| Net Weight | 1.700 KG |
| Dimensions | 35 × 24 × 2 cm |
| Plant | 0001 – AN PLANT – BENGALURU |
| Sales Organization | 0001 – Sales Org. 001 |
| Distribution Channel | 01 – Distribution Channel 01 |
| Classification | Class Type 001 / Class 1000 |
| Tax Classification | 1 – Full tax for displayed entries |
| Availability Check | 02 – Individual requirements |
| Profit Center | PC0001 |
| Inventory Planning Mode | eSPP calculation |
| Loading Group | 0002 – Forklift |
| Transportation Group | 0004 – Parcel |
| Material Status | **Active project material — 194** |

The material master is a shared SAP business object. Its different views support procurement, inventory, sales, planning, logistics, and accounting-related processes.

## Material Master Documentation

Detailed implementation documentation is maintained in:

`docs/mm/material-194-tech-nova-business-laptop.md`

## O2C Dependency

Material 194 is the current product identifier for the project's Sales Order 12 milestone:

```text
Material 194
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
```

## Planned MM Scope

The wider MM process will continue through procurement, goods receipt, inventory validation, invoice verification, and FI/CO integration. Those activities will be marked complete only after execution and validation in SAP.

## Evidence

MM evidence is maintained under:

`evidence/screenshots/mm/`

The current upload does not include a new standalone MM screenshot set proving Material 194, so the repository does not fabricate screenshot evidence. The new uploaded screenshots are stored under the SD-FI billing-resolution evidence area.

## Current Status

**Status: In Progress**

Material Master documentation and the downstream Sales Order reference have been revised to Material **194**.
