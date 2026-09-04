# Materials Management (MM)

## 1. Current MM Implementation

The active TechNova laptop material is **194 — TechNova Business Laptop**. The MM workstream now covers the material-master foundation, inbound procurement, Goods Receipt, invoice verification, and vendor settlement evidence documented in the completed P2P lifecycle.

## 2. Material 194 Profile

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

## 3. O2C Dependency

Material `194` is the current product identifier used by the completed core O2C scenario, which progressed through Sales Order `18` and downstream logistics and financial execution:

```text
Material 194
   ↓
MM03 Verification
   ↓
MM02 Shipping Data
   ↓
Shipping Point Determination
   ↓
VA01 Sales Order 18
   ↓
VL01N / VL02N
   ↓
VF01 Billing
```

## 4. Inbound Procurement & Goods Receipt

The inbound logistics scenario uses Purchase Order `4500000149`.

| Field | Value |
|---|---|
| Purchase Order | `4500000149` |
| Vendor | Apex Industrial Supplies GmbH |
| Material | TechNova 15.6" Display Panel |
| Quantity | `10 EA` |
| Cost Center | `CC9000` |
| Profit Center | `PC9000` |
| Target G/L Account | `5010032` |

### 4.1 Goods Receipt — `MIGO`

The Goods Receipt was executed using:

- Transaction: `MIGO`
- Business Operation: `A01` — Goods Receipt
- Reference: `R01` — Purchase Order
- Movement Type: `101`
- Purchase Order: `4500000149`
- Quantity: `10 EA`
- Material Document: `5000000062`
- Posting Date: `30.08.2026`

### 4.2 P2P Invoice Verification & Settlement

The subsequent procurement steps were completed and documented:

```text
MIGO / Material Document 5000000062
        ↓
MIRO / Logistics Invoice 5105600101
        ↓
FI Document 5100000000
        ↓
F-53 / Payment Document 5000000000
        ↓
Vendor Clearing
        ↓
Vendor Balance = €0.00
```

The completed P2P case records a net procurement value of `€500.00`, input VAT of `€95.00`, and gross payable of `€595.00`, with the documented GR/IR and vendor balances reconciled to `€0.00`.

## 5. PP / Manufacturing Dependency

Material `194` is also used as the finished product in the completed Plan-to-Produce execution case:

```text
Production Order 1000020
        ↓
CO15 — 10 EA Confirmation
        ↓
MIGO — Movement 101
        ↓
Material Document 5000000063
        ↓
MMBE — 95 EA Unrestricted Stock
```

This demonstrates the shared role of the material master across MM, PP, inventory, and controlling processes.

## 6. Integration Dependency

```text
CO / Universal Journal Prerequisite
        ↓
Posting Block Resolved
        ↓
Purchase Order 4500000149
        ↓
MIGO — Goods Receipt 101
        ↓
Material Document 5000000062
        ↓
MIRO — Invoice Verification
        ↓
FI / AP
        ↓
F-53 — Vendor Payment
        ↓
Vendor Clearing
```

This illustrates how financial-system consistency can become a prerequisite for successful operational posting.

## 7. Evidence

MM/P2P evidence is maintained under:

`08-evidence/screenshots/p2p/`

The associated evidence pack is:

`08-evidence/evidence-packs/p2p-lifecycle-report.md`

## 8. Current Status

**Status: Completed for the documented P2P execution.**

Material `194` remains the active core project material. The inbound procurement scenario is complete through Goods Receipt, MIRO invoice verification, FI verification, F-53 payment, and vendor clearing.
