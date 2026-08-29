# SAP Evidence Screenshot Manifest

Updated: **29 August 2026**

This manifest separates master-data evidence, SD execution evidence, and the newly integrated SD-FI billing-resolution evidence.

## MM — Current Material 194

The active material identifier is **194 — TechNova Business Laptop**. Previous references to the retired identifier have been removed from the active documentation.

Expected evidence naming standard for the current material:

| Screenshot | SAP step |
|---|---|
| `material-194-created.png` | Material creation confirmation |
| `material-194-basic-data.png` | Basic Data |
| `material-194-organizational-levels.png` | Plant / Sales Organization / Distribution Channel |
| `material-194-classification-1000.png` | Class Type `001` / Class `1000` |
| `material-194-sales-tax.png` | Sales Organization 1 / tax classification |
| `material-194-sales-org-2-item-category-review.png` | Sales Organization 2 review |
| `material-194-plant-profit-center.png` | Plant data / Profit Center `PC0001` |
| `material-194-spp-basic-data.png` | Extended SPP Basic Data |
| `material-194-purchasing-material-group-validation.png` | Purchasing validation |
| `material-194-mm03-general-plant.jpg` | `MM03` verification |
| `material-194-loading-group-0002.jpg` | `MM02` Loading Group `0002` |
| `material-194-transportation-group-0004.jpg` | `MM02` Transportation Group `0004` |

> The current upload does not contain a new standalone MM screenshot set proving Material 194. The documentation has therefore been updated to 194 without fabricating screenshot evidence.

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

## SD-FI — Billing Resolution Evidence

The new billing-resolution evidence is stored under:

`evidence/screenshots/sd/billing-resolution/`

| File | Step |
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
| `19_vf02_successful_release.png` | Final VF02 release to accounting |
| `20_fb03_posted_document.png` | FB03 posted FI document |

## Source Document

`evidence/implementation-evidence-packs/SAP_SD_FI_Billing_Release_Documentation.pdf`

The final release and accounting-verification evidence is documented in the supplied PDF. Standalone final screenshots `19` and `20` were extracted from that evidence package for easier repository navigation.
