# Material Master — 184 — TechNova Business Laptop

## My Implementation Overview

I created material **184**, **TechNova Business Laptop**, as a finished product master for the SAP Business Suite end-to-end project. I created the material so that the same business object can later participate in sales, procurement, inventory, planning, logistics, and accounting processes.

The material-master exercise demonstrates why SAP master data is maintained across multiple views: different business functions consume different parts of the same material record.

## 1. Initial Material Setup

| Field | Value | Why I maintained it |
|---|---|---|
| Material | `184` | Unique SAP identifier for the product |
| Description | `TechNova Business Laptop` | Business-readable product description |
| Material Type | `Finished Product` | Represents the laptop as an end product |
| Industry | `Mechanical engineering` | Industry selection available during creation |
| Base Unit | `EA – Each` | I manage the laptop as an individual unit |

I selected the relevant material views because the material needs to support sales-area data, plant/logistics data, purchasing data, classification, and planning-related information.

## 2. Basic Product Data

| Field | Value | Business Purpose |
|---|---|---|
| Gross Weight | `2 KG` | Supports logistics and shipping information |
| Net Weight | `1.700 KG` | Represents product weight excluding packaging |
| Size / Dimensions | `35 × 24 × 2 cm` | Provides physical product information |

I maintained these values in the material's basic-data views so the product has usable physical and logistics attributes.

## 3. Organizational Extensions

The material was extended to the organizational levels shown during the material-creation workflow:

| Organizational Object | Value | Purpose |
|---|---|---|
| Plant | `0001 – AN PLANT – BENGALURU` | Connects the material to a plant |
| Sales Organization | `0001 – Sales Org. 001` | Defines the sales organization responsible for selling |
| Distribution Channel | `01 – Distribution Channel 01` | Defines the sales route/channel |

I used these organizational levels because SAP applies operational material settings according to the relevant organizational context.

> **Project evidence note:** These are the organizational values explicitly recorded in the material-master workflow. I am not replacing them with other project values that were not shown in this material-creation evidence.

## 4. Classification

I assigned material **184** to:

| Field | Value |
|---|---|
| Class Type | `001 – Material Class` |
| Class | `1000` |

I used classification to provide a structured way of grouping the material beyond its description and material number. This can support later searching, organization, and characteristic-based handling of the product.

## 5. Sales Organization 1 — Sales and Tax Data

I opened the Sales Organization 1 view for Sales Organization `0001` and Distribution Channel `01`.

### Tax Classification

The available tax-classification values included:

- `0` — No tax
- `1` — Full tax
- `2` — Half tax
- `3` — Low tax rate
- `4` — Mixed taxes

I selected **`1 – Full tax`** for the displayed tax entries.

The tax table displayed entries for **Germany and India**, including output-tax condition types. I maintained the classification visible in the workflow and continued to the next views.

The material master supplies the classification used by the sales/tax determination logic; the actual tax calculation remains dependent on the system's tax configuration.

## 6. Sales Organization 2 — Item Category Review

I opened the Sales Organization 2 view and reviewed the **Item Category Group** value help.

The system displayed standard SAP options covering different sales-order behaviors, including standard items, third-party items, credit memo items, configuration products, and service-related categories.

I reviewed the available catalogue to validate which sales behavior is available for the finished product. I do **not** record an Item Category Group as assigned because the project evidence does not establish a final selected value.

## 7. General / Plant Data — Logistics and Profit Center

For Plant `0001 – AN PLANT – BENGALURU`, I maintained/reviewed the following values:

| Field | Value | Purpose |
|---|---|---|
| Plant | `0001 – AN PLANT – BENGALURU` | Plant-specific material extension |
| Availability Check | `02 – Individual requirements` | Controls how material availability is checked |
| Profit Center | `PC0001` | Supports profit-center reporting/accounting integration |
| Base Unit | `EA` | Inventory and logistics quantity is managed in individual units |

I used the Profit Center value help and selected **PC0001**. The system displayed controlling area `0001`, the name **TECHNOVA BENGALURU**, and responsible-person information including Ravi Kiran before I selected the entry.

## 8. Extended SPP Basic Data

I reviewed the **Extended SPP Basic Data** view because it is relevant to supply and inventory planning.

The Planning Scenario section displayed options such as:

- Product for Kit-to-Order
- Procure to Order
- Push Deployment from Supplier
- Inventory Balancing Not Allowed
- Other planning scenarios

No planning scenario was selected in the captured workflow.

The Inventory Planning Mode displayed **eSPP calculation**.

I left surplus/obsolescence and production/warranty/recall/goodwill date fields unchanged because no project-specific requirement for those values was established in the workflow.

## 9. International Trade — Export

I reviewed the International Trade: Export view, including fields for:

- Intrastat Group
- CAS Number
- PRODCOM Number
- Control Code
- Country/Region of Origin

The captured workflow showed these fields blank. I therefore did not invent regulatory values that were not provided by the project requirements.

## 10. Sales Text

I reviewed the Sales Text view for Sales Organization `0001` / Distribution Channel `01`.

English was listed as the maintained language, and SAP indicated that no sales text was maintained. I did not add artificial marketing text because no approved project wording had been specified.

## 11. Purchasing View — Mandatory Field Validation

I moved to the Purchasing view for Plant `0001`.

SAP stopped the process with the validation message:

> **Make an entry in mandatory field 'Material Group'.**

I used the Material Group value help instead of inventing a code manually. SAP displayed a catalogue of **185 material groups**, including examples such as `01`, `02`, and `1000 Steel Raw Material`.

I selected a valid Material Group from the system catalogue, which resolved the mandatory-field validation and allowed the material to be saved successfully.

The final evidence confirms that a Material Group was selected, but it does **not** clearly preserve the exact selected code. I therefore do not guess the code in this documentation.

## 12. Final Material Creation

After I completed the required material data and resolved the mandatory Material Group validation, I saved the material.

SAP returned the confirmation:

**Material 184 created**

This confirms successful creation of the material master record.

## 13. Business and Integration Value

I created this material as a shared master-data object that can later be consumed by multiple integrated processes.

The current material setup prepares the product for:

- **Sales** — sales-area data and tax classification
- **Procurement** — purchasing view and material grouping
- **Inventory and Logistics** — plant extension, unit, weight, and availability data
- **Planning** — Extended SPP review
- **Management Accounting** — profit-center assignment
- **Classification** — material class `1000`
- **Future End-to-End Testing** — use of material `184` across integrated business scenarios

The exercise demonstrates the principle that a material is created once but its master data is consumed by multiple SAP business processes.

## 14. Completed Work

| Work Performed | Result |
|---|---|
| Initial material setup | Completed |
| Material 184 / TechNova Business Laptop | Created |
| Basic product data | Maintained |
| Plant 0001 extension | Extended |
| Sales Organization 0001 / Distribution Channel 01 | Extended |
| Classification 001 / Class 1000 | Assigned |
| Sales and tax data | Maintained |
| Profit Center PC0001 | Assigned |
| Extended SPP view | Reviewed |
| Export / foreign-trade view | Reviewed |
| Sales text | Reviewed |
| Purchasing / Material Group validation | Resolved |
| Material save | **SUCCESS** |

## 15. Next Verification Step

Before I continue to the next business process, I will use **MM03 – Display Material** to verify that material `184` exists independently after creation and to review the key views without changing the master data.

After that verification, I can continue the end-to-end scenario from the material master into the next relevant procurement, inventory, or sales process.

> **Documentation principle:** I record only values and results supported by the captured SAP workflow. Where the evidence does not preserve an exact value, I explicitly mark it as not established rather than guessing.

## Evidence

I will maintain MM screenshots for this material under:

`evidence/screenshots/mm/`

Recommended filenames:

- `material-184-created.png`
- `material-184-basic-data.png`
- `material-184-organizational-levels.png`
- `material-184-classification-1000.png`
- `material-184-sales-tax.png`
- `material-184-sales-org-2-item-category-review.png`
- `material-184-plant-profit-center.png`
- `material-184-spp-basic-data.png`
- `material-184-purchasing-material-group-validation.png`
- `material-184-mm03-verification.png`
