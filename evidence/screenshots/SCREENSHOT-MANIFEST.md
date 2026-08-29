# SAP Evidence Screenshot Manifest

Updated: **29 August 2026**

This manifest separates master-data evidence, SD execution evidence, and the integrated SD-FI billing-resolution evidence.

## MM — Current Material 194

The active material identifier is **194 — TechNova Business Laptop**.

| Screenshot | SAP step |
|---|---|
| `material-194-created.png` | Material creation confirmation |
| `material-194-basic-data.png` | Basic Data |
| `material-194-organizational-levels.png` | Plant / Sales Organization / Distribution Channel |
| `material-194-classification-1000.png` | Class Type `001` / Class `1000` |
| `material-194-sales-tax.png` | Sales Organization / tax classification |
| `material-194-sales-org-2-item-category-review.png` | Sales Organization 2 review |
| `material-194-plant-profit-center.png` | Plant data / Profit Center `PC0001` |
| `material-194-spp-basic-data.png` | Extended SPP Basic Data |
| `material-194-purchasing-material-group-validation.png` | Purchasing validation |
| `material-194-mm03-general-plant.jpg` | `MM03` verification |
| `material-194-loading-group-0002.jpg` | `MM02` Loading Group `0002` |
| `material-194-transportation-group-0004.jpg` | `MM02` Transportation Group `0004` |

## SD — Sales Order 12

| Evidence | SAP step |
|---|---|
| `shipping-point-determination-overview.jpg` | Shipping Point Determination overview |
| `shipping-point-determination-saved.jpg` | Saved determination |
| `sales-order-shipping-determined.jpg` | `VA01` shipping point |
| `sales-order-save-incomplete.jpg` | `VA01` incompletion warning |
| `sales-order-incompletion-log.jpg` | Net Value missing |
| `sales-order-pricing-condition-help.jpg` | PR00 value help |
| `sales-order-pr00-price.jpg` | PR00 maintained |
| `sales-order-12-saved.jpg` | Sales Order 12 saved |

## SD-FI — Billing Resolution Source Package

The uploaded billing update contains **18 SAP screenshots**. Their intended repository location is:

`evidence/screenshots/sd/billing-resolution/`

| Source file | SAP step |
|---|---|
| `01_vf02_billing_error_initial.png` | Initial VF02 account-determination error |
| `02_vf02_release_to_accounting_click.png` | VF02 release action |
| `03_vkoa_table005_acct_key_overview.png` | VKOA Table 005 overview |
| `04_vkoa_table005_erl_revenue_entry_saved.png` | ERL revenue mapping saved |
| `05_vf02_tax_determination_error_t030k_mws.png` | T030K / MWS tax error |
| `06_ob40_automatic_posting_procedures_list.png` | OB40 posting procedures |
| `07_ob40_mws_output_tax_rules_bkmg.png` | MWS rules for BKMG |
| `08_ob40_save_rules_prompt.png` | OB40 save confirmation |
| `09_ob40_mws_account_assignment_screen.png` | MWS account assignment |
| `10_ob40_mws_account_2300000_saved.png` | G/L 2300000 assignment saved |
| `11_vf02_gl_2300000_not_defined_bkmg.png` | Missing G/L 2300000 error |
| `12_fs00_create_gl_2300000_initial.png` | FS00 G/L creation |
| `13_fs00_gl_2300000_type_description.png` | G/L type and description |
| `14_fs00_gl_2300000_control_data.png` | G/L control data |
| `15_fs00_gl_2300000_create_bank_interest.png` | Bank/interest settings |
| `16_fs00_gl_2300000_cash_flow_validation.png` | Cash-flow validation |
| `17_fs00_gl_2300000_saved_display.png` | G/L 2300000 saved |
| `18_vf02_gl_6010131_not_defined_cocode_9000.png` | Missing revenue G/L error |

## Final-Stage Evidence

The supplied PDF documents the later stages as completed:

- FBN1 — number range Z1 for fiscal year 2026
- VF02 — successful release of billing document 90000032
- FB03 — FI document 9000000000 and balanced journal entry
- FBL5N — identified as the next customer open-item verification step
- F-28 — identified as the next incoming-payment clearing step

The source PDF is the authoritative evidence package for these stages. No standalone SAP screenshot is claimed here unless it is actually present in the supplied source files.

## Source Document

`evidence/implementation-evidence-packs/SAP_SD_FI_Billing_Release_Documentation.pdf`

## Material Governance

The core O2C project uses **Material 194 — TechNova Business Laptop**. The supplied billing evidence records **10194**; that source identifier is preserved in the billing case study for traceability.
