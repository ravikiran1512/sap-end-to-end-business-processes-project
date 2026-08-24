# SAP Business Suite Project — Material Verification to Sales Order

**Project:** TechNova SAP End-to-End Business Process Implementation  
**Execution date:** 24 August 2026  
**Scenario:** Material 184 — TechNova Business Laptop  
**Sales Order:** 12  
**Customer:** 1000000020 — TechNova GmbH

## 1. Purpose

This evidence record extends the previous Material Master milestone. Material **184** had already been created successfully. This session verifies the material, completes the shipping-related material data used by the practice-system sales process, validates shipping-point determination, and creates a sales order.

> **Environment note:** The screenshots record execution in the available SAP practice/server environment. Values such as Plant `0001`, Shipping Point `0001`, and customer `1000000020` are captured as executed system values. They are not silently reclassified as the confirmed TechNova enterprise IDs in the project master plan.

## 2. Material Verification — MM03

`MM03` — Display Material was used to verify Material **184 — TechNova Business Laptop** after creation.

| Field | Verified value |
|---|---|
| Material | `184` |
| Description | `TechNova Business Laptop` |
| Plant | `0001 — AN PLANT – BENGALURU` |
| Base Unit | `EA — Each` |
| Gross Weight | `2 KG` |
| Net Weight | `1.700 KG` |
| Availability Check | `02 — Individual requirements` |
| Profit Center | `PC0001` |

**Screenshot:** `material-184-mm03-general-plant.jpg`

## 3. Shipping-Relevant Material Data — MM02

The material was opened in `MM02` to maintain shipping data required for the executed sales/delivery scenario.

### Loading Group

SAP value help showed `0001 — Crane`, `0002 — Forklift`, and `0003 — Manual`. Material 184 was maintained with **Loading Group `0002 — Forklift`**.

**Screenshot:** `material-184-loading-group-0002.jpg`

### Transportation Group

SAP value help included `0001 — On pallets`, `0002 — In liquid form`, `0003 — Container`, `0004 — Parcel`, `0005 — Bulk Product`, and `TVS1 — On pallets`. Material 184 was maintained with **Transportation Group `0004 — Parcel`**.

**Screenshot:** `material-184-transportation-group-0004.jpg`

The material was saved successfully.

## 4. Shipping Point Determination

The sales process initially could not determine a shipping point. The Shipping Point Determination view was therefore checked and the executed combination was added/saved:

| Determination field | Value |
|---|---|
| Shipping Condition | `01` |
| Loading Group | `0002` |
| Plant | `0001` |
| Proposed Shipping Point | `0001` |

**Screenshots:**

- `shipping-point-determination-overview.jpg`
- `shipping-point-determination-saved.jpg`

This is an important SD/Logistics Execution integration point because the shipping condition, loading group, and delivering plant participate in shipping-point determination for the outbound delivery process.

## 5. Sales Order Creation — VA01

`VA01` — Create Standard Order was used to create the customer order.

| Field | Value |
|---|---|
| Sales Document Type | Standard Order |
| Sold-to Party | `1000000020` — TechNova GmbH |
| Ship-to Party | `1000000020` — TechNova GmbH |
| Customer Reference | `TECHNOVA-001` |
| Material | `184` — TechNova Business Laptop |
| Order Quantity | `10 EA` |
| Delivering Plant | `0001 — AN PLANT – BENGALURU` |

After the shipping-point determination correction, the sales-order item was able to determine Shipping Point `0001`.

**Screenshot:** `sales-order-shipping-determined.jpg`

## 6. Incompletion Handling and Pricing

The first save attempt reported that the document was incomplete because **Net Value** was missing.

**Screenshot:** `sales-order-save-incomplete.jpg`

The Incompletion Log identified **Net Value** as missing for item `10`.

**Screenshot:** `sales-order-incompletion-log.jpg`

The item pricing was then completed with **PR00 — Price**. The maintained price was **1.00 EUR per EA** for **10 EA**, resulting in a **10.00 EUR** net value.

**Screenshot:** `sales-order-pr00-price.jpg`

## 7. Final Result

The sales order was saved successfully.

> **Standard order 12 has been saved.**

Final executed values:

- Sales Order: **12**
- Customer: **1000000020 — TechNova GmbH**
- Material: **184 — TechNova Business Laptop**
- Quantity: **10 EA**
- Price: **1.00 EUR / EA**
- Net Value: **10.00 EUR**
- Customer Reference: **TECHNOVA-001**

**Screenshot:** `sales-order-12-saved.jpg`

## 8. Business Process Position

```text
Material Master 184
       ↓
MM03 Material Verification
       ↓
MM02 Shipping Data
       ↓
Shipping Point Determination
       ↓
VA01 Sales Order 12
       ↓
[Next] VL01N Outbound Delivery
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

The sales order is not an isolated SD transaction. It depends on material master data and configuration maintained earlier. The loading group participates in shipping-point determination, the delivering plant connects the sales item to logistics execution, shipping-point determination enables the delivery step, and pricing conditions determine the order's net value.

## 10. Evidence Status

| Milestone | Status | Evidence |
|---|---|---|
| Material 184 exists after creation | Completed | MM03 |
| Loading Group 0002 maintained | Completed | MM02 |
| Transportation Group 0004 maintained | Completed | MM02 |
| Shipping Point Determination | Completed in practice system | SD configuration |
| Sales Order 12 created | **Completed** | VA01 final confirmation |
| Outbound Delivery | Next | `VL01N` |
| Picking | Pending | — |
| Post Goods Issue | Pending | — |
| Billing | Pending | — |
| FI/AR integration validation | Pending | — |

See `evidence/screenshots/SCREENSHOT-MANIFEST.md` for the complete screenshot list and the accompanying screenshot package for the captured images.

---

**Repository evidence rule:** This document records what was actually executed and visible in SAP. It does not infer undocumented configuration values or convert practice-system/demo IDs into confirmed TechNova configuration IDs.
