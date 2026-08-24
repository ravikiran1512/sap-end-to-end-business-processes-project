# SAP Business Suite Project — Material Verification to Sales Order 12

**Project:** TechNova SAP End-to-End Business Process Implementation  
**Execution date:** 24 August 2026  
**Scenario:** Material 184 — TechNova Business Laptop  
**Sales Order:** 12  
**Customer:** 1000000020 — TechNova GmbH

## 1. Purpose

I extended the completed Material Master milestone into the first executed Order-to-Cash milestone. I verified Material **184**, maintained the shipping-related material data required by the executed sales process, corrected the shipping-point determination needed by the scenario, and created Sales Order **12**.

> **Environment note:** The screenshots record execution in the available SAP practice/server environment. Values such as Plant `0001`, Shipping Point `0001`, and customer `1000000020` are recorded as executed system values. I do not silently reclassify them as the confirmed TechNova enterprise IDs in the project master plan.

## 2. Material Verification — MM03

### Transaction

`MM03` — Display Material

I used MM03 to verify Material **184 — TechNova Business Laptop** after its creation.

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

The MM03 display confirmed that the material record exists after creation and that the key plant/general data required for the subsequent sales execution is available.

**Evidence:** `evidence/screenshots/mm/material-184-mm03-general-plant.jpg`

## 3. Shipping-Relevant Material Data — MM02

### Transaction

`MM02` — Change Material

I opened Material 184 in change mode to maintain the shipping data required by the executed sales/delivery scenario.

### Loading Group

The SAP value help showed:

- `0001` — Crane
- `0002` — Forklift
- `0003` — Manual

I selected **Loading Group `0002 — Forklift`** for Material 184.

**Evidence:** `evidence/screenshots/mm/material-184-loading-group-0002.jpg`

### Transportation Group

The SAP value help showed entries including:

- `0001` — On pallets
- `0002` — In liquid form
- `0003` — Container
- `0004` — Parcel
- `0005` — Bulk Product
- `TVS1` — On pallets

I selected **Transportation Group `0004 — Parcel`** for Material 184 and saved the material.

**Evidence:** `evidence/screenshots/mm/material-184-transportation-group-0004.jpg`

I maintained these values because the loading group participates in the shipping-point determination used by the sales and outbound-delivery process.

## 4. Shipping Point Determination

During the first sales-order attempt, SAP could not determine a shipping point for the item. I therefore checked the Shipping Point Determination configuration and added the combination required by the executed scenario.

| Determination field | Value |
|---|---|
| Shipping Condition | `01` |
| Loading Group | `0002` |
| Plant | `0001` |
| Proposed Shipping Point | `0001` |

I saved the new entry successfully.

**Evidence:**

- `evidence/screenshots/sd/shipping-point-determination-overview.jpg`
- `evidence/screenshots/sd/shipping-point-determination-saved.jpg`

### Why I performed this configuration

Shipping-point determination is an SD/Logistics Execution integration point. SAP uses the shipping condition, loading group, and delivering plant to determine the shipping point that will be used for the outbound delivery process.

## 5. Sales Order Creation — VA01

### Transaction

`VA01` — Create Standard Order

I used VA01 to create the customer order after correcting the shipping-point determination.

### Header and Item Data

| Field | Value |
|---|---|
| Sales Document Type | Standard Order |
| Sold-to Party | `1000000020` — TechNova GmbH |
| Ship-to Party | `1000000020` — TechNova GmbH |
| Customer Reference | `TECHNOVA-001` |
| Material | `184` — TechNova Business Laptop |
| Order Quantity | `10 EA` |
| Delivering Plant | `0001 — AN PLANT – BENGALURU` |

After I corrected shipping-point determination, SAP was able to populate the expected shipping information for the sales-order item.

**Evidence:** `evidence/screenshots/sd/sales-order-shipping-determined.jpg`

## 6. Incompletion Handling and Pricing

When I first attempted to save the order, SAP reported that the document was incomplete because the **Net Value** was missing.

**Evidence:** `evidence/screenshots/sd/sales-order-save-incomplete.jpg`

I opened the Incompletion Log and identified **Net Value** as missing for item `10`.

**Evidence:** `evidence/screenshots/sd/sales-order-incompletion-log.jpg`

I then opened the item pricing screen and reviewed the condition value help. I selected the standard price condition **PR00 — Price**.

I maintained:

- **Amount:** `1.00 EUR`
- **Per:** `1 EA`
- **Quantity:** `10 EA`
- **Net Value:** `10.00 EUR`

**Evidence:** `evidence/screenshots/sd/sales-order-pricing-condition-help.jpg` and `evidence/screenshots/sd/sales-order-pr00-price.jpg`

### Why I corrected the incompletion

I needed a valid net value before SAP could save the order as a complete sales document. By maintaining PR00, I provided the pricing information required for the executed scenario and resolved the incompletion item.

## 7. Final Result

After I completed the missing pricing information, I saved the sales order successfully.

> **Standard order 12 has been saved.**

The final executed order contains:

- Sales Order: **12**
- Customer: **1000000020 — TechNova GmbH**
- Material: **184 — TechNova Business Laptop**
- Quantity: **10 EA**
- Price: **1.00 EUR / EA**
- Net Value: **10.00 EUR**
- Customer Reference: **TECHNOVA-001**

**Evidence:** `evidence/screenshots/sd/sales-order-12-saved.jpg`

## 8. Business Process Position

The completed execution establishes this document/process chain:

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

This milestone demonstrated to me that a sales order is not an isolated SD transaction.

I used material master data that I had created and verified earlier. I used the loading group in shipping-point determination, connected the sales item to the delivering plant, corrected the shipping-point configuration when SAP could not determine it, and maintained pricing so that the order could be completed.

The Sales Order now becomes the reference document for the next logistics step: **VL01N — Create Outbound Delivery**.

## 10. Evidence Status

| Milestone | Status | Evidence |
|---|---|---|
| Material 184 exists after creation | **Completed** | MM03 |
| Loading Group 0002 maintained | **Completed** | MM02 |
| Transportation Group 0004 maintained | **Completed** | MM02 |
| Shipping Point Determination | **Completed in practice system** | SD configuration |
| Sales Order 12 created | **Completed** | VA01 final confirmation |
| Outbound Delivery | **Next** | `VL01N` |
| Picking | Pending | — |
| Post Goods Issue | Pending | — |
| Billing | Pending | — |
| FI/AR integration validation | Pending | — |

## 11. Next Execution Step

My next SAP transaction is:

**`VL01N` — Create Outbound Delivery**

I will create the outbound delivery with reference to **Sales Order 12** and then document the delivery, picking, goods issue, billing, and FI/AR integration steps only after I execute and validate them in SAP.

> **Repository evidence rule:** I record what I actually execute and what SAP displays. I do not infer undocumented configuration values or convert practice-system/demo IDs into confirmed TechNova configuration IDs.
