# Material Verification → Sales Order 12 — Screenshot Manifest

Execution date: **24 August 2026**

I captured the screenshots for this milestone during the SAP GUI execution session. I organize the evidence by SAP module so that each screenshot can be traced to the implementation step it supports.

## MM evidence — Material 184

### Existing Material Master evidence

| Screenshot | SAP step |
|---|---|
| `material-184-created.png` | Material creation confirmation — **Material 184 created** |
| `material-184-basic-data.png` | Material 184 — Basic Data 1 |
| `material-184-organizational-levels.png` | Material creation — Plant `0001`, Sales Organization `0001`, Distribution Channel `01` |
| `material-184-classification-1000.png` | Classification — Class Type `001`, Class `1000` |
| `material-184-sales-tax.png` | Sales Organization 1 — tax classification evidence |
| `material-184-sales-org-2-item-category-review.png` | Sales Organization 2 — Item Category Group value-help review |
| `material-184-plant-profit-center.png` | General/Plant data — Profit Center `PC0001` |
| `material-184-spp-basic-data.png` | Extended SPP Basic Data — eSPP calculation |
| `material-184-purchasing-material-group-validation.png` | Purchasing — mandatory Material Group validation |

### Post-creation / O2C preparation evidence

| Screenshot | SAP step |
|---|---|
| `material-184-mm03-general-plant.jpg` | `MM03` — Material 184 verification |
| `material-184-loading-group-0002.jpg` | `MM02` — Loading Group `0002 — Forklift` |
| `material-184-transportation-group-0004.jpg` | `MM02` — Transportation Group `0004 — Parcel` |

## SD evidence — Sales Order 12

| Screenshot | SAP step |
|---|---|
| `shipping-point-determination-overview.jpg` | Shipping Point Determination configuration overview |
| `shipping-point-determination-saved.jpg` | Saved Shipping Point Determination entry |
| `sales-order-shipping-determined.jpg` | `VA01` — Shipping Point determined for item |
| `sales-order-save-incomplete.jpg` | `VA01` — Incomplete document warning |
| `sales-order-incompletion-log.jpg` | `VA01` — Net Value missing for item 10 |
| `sales-order-pricing-condition-help.jpg` | `VA01` — Pricing condition value-help review |
| `sales-order-pr00-price.jpg` | `VA01` — PR00 maintained at `1.00 EUR/EA` |
| `sales-order-12-saved.jpg` | `VA01` — Standard Order 12 saved successfully |

## Evidence source

The uploaded evidence record and PDF document describe the execution from MM03 verification through Sales Order 12 creation. I use those documents as the source for the filenames and SAP-step mapping.

## Next evidence milestone

The next SAP execution step is:

**`VL01N` — Create Outbound Delivery with reference to Sales Order 12.**

I will add the VL01N screenshots to `evidence/screenshots/sd/` when I execute and capture that step.

## Important

I keep practice/server values such as Plant `0001`, Shipping Point `0001`, and customer `1000000020` traceable to the executed evidence. I do not silently convert them into confirmed TechNova enterprise IDs.

Before public publication, I will review screenshots for credentials, connection details, server information, or other sensitive environment data.
