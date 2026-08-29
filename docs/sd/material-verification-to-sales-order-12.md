# SAP Business Suite Project — Material Verification to Sales Order 12

**Project:** TechNova SAP End-to-End Business Process Implementation  
**Execution date:** 24 August 2026  
**Current Material:** **194 — TechNova Business Laptop**  
**Sales Order:** **12**  
**Customer:** `1000000020 — TechNova GmbH`

> **Master-data revision:** The project's previous material identifier has been replaced by **194**. All active documentation now uses Material 194.

## 1. Purpose

This milestone connects Material Master data with the first executed Order-to-Cash activity. The material was verified, shipping-relevant data was maintained, shipping-point determination was corrected for the practice scenario, and Standard Sales Order **12** was created.

## 2. Material Verification — MM03

`MM03 — Display Material`

| Field | Current value |
|---|---|
| Material | `194` |
| Description | `TechNova Business Laptop` |
| Plant | `0001 — AN PLANT – BENGALURU` |
| Base Unit | `EA — Each` |
| Gross Weight | `2 KG` |
| Net Weight | `1.700 KG` |
| Availability Check | `02 — Individual requirements` |
| Profit Center | `PC0001` |

## 3. Shipping-Relevant Material Data — MM02

The shipping attributes required by the executed scenario are:

- Loading Group: **`0002 — Forklift`**
- Transportation Group: **`0004 — Parcel`**

The loading group participates in shipping-point determination together with shipping condition and delivering plant.

## 4. Shipping Point Determination

The executed practice-system combination is:

| Determination field | Value |
|---|---|
| Shipping Condition | `01` |
| Loading Group | `0002` |
| Plant | `0001` |
| Proposed Shipping Point | `0001` |

The configuration was added/saved after the first sales-order attempt could not determine a shipping point.

## 5. Sales Order Creation — VA01

| Field | Executed value |
|---|---|
| Sales Document Type | Standard Order |
| Sold-to Party | `1000000020 — TechNova GmbH` |
| Ship-to Party | `1000000020 — TechNova GmbH` |
| Customer Reference | `TECHNOVA-001` |
| Material | **`194 — TechNova Business Laptop`** |
| Order Quantity | `10 EA` |
| Delivering Plant | `0001 — AN PLANT – BENGALURU` |
| Shipping Point | `0001` |

## 6. Incompletion Handling and Pricing

The first save attempt reported a missing **Net Value**. The Incompletion Log identified the missing value for item `10`.

The standard pricing condition **PR00 — Price** was maintained as follows:

- Amount: `1.00 EUR`
- Per: `1 EA`
- Quantity: `10 EA`
- Net Value: `10.00 EUR`

This resolved the order incompletion and allowed the document to be saved.

## 7. Final Result

SAP confirmed:

> **Standard order 12 has been saved.**

Final executed order:

| Attribute | Result |
|---|---|
| Sales Order | **12** |
| Customer | `1000000020 — TechNova GmbH` |
| Material | **194 — TechNova Business Laptop** |
| Quantity | `10 EA` |
| Price | `1.00 EUR / EA` |
| Net Value | `10.00 EUR` |
| Customer Reference | `TECHNOVA-001` |
| Delivering Plant | `0001` |
| Shipping Point | `0001` |

## 8. Business Process Position

```text
Material 194
       ↓
MM03 Verification                 ✓
       ↓
MM02 Shipping Data               ✓
       ↓
Shipping Point Determination     ✓
       ↓
VA01 Sales Order 12              ✓
       ↓
VL01N Outbound Delivery          ← NEXT
       ↓
Picking
       ↓
Post Goods Issue
       ↓
Billing
       ↓
FI / Accounts Receivable Impact
```

## 9. Implementation Learning

This milestone demonstrates the dependency chain between master data, SD configuration, and transactional execution. Material master attributes feed logistics determination, the shipping point enables delivery execution, and pricing completeness is required before the sales order can be saved.

## 10. Next Execution Step

**`VL01N — Create Outbound Delivery`** with reference to Sales Order **12**.

The subsequent picking, Post Goods Issue, billing, and FI/Accounts Receivable steps will be documented only after they are executed and validated in SAP.
