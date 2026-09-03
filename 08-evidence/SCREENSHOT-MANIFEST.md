# SAP Screenshot Manifest

This manifest indexes the current process-oriented screenshot evidence stored under `08-evidence/screenshots/`.

## O2C — Core Lifecycle

Target folder: `08-evidence/screenshots/o2c/`

| # | Screenshot | SAP Evidence |
|---:|---|---|
| 01 | `01_MMPV_Period_Closed_Error_M7053.png` | PGI blocked because period `09/2026` was not open |
| 02 | `02_MMPV_Close_Period_Selection.png` | `MMPV` period-roll-forward parameters |
| 03 | `03_MMPV_Execution_Log.png` | Successful MM period conversion to `09/2026` |
| 04 | `04_OBYC_Account_Determination_Error_GBB_VAX.png` | Error `M8 147` for missing `BKMG / GBB / 0001 / VAX / 7920` |
| 05 | `05_OBYC_BSX_Inventory_Posting.png` | Inventory posting/account-determination review |
| 06 | `06_OBYC_GBB_Maintenance_Initial.png` | Initial GBB configuration review |
| 07 | `07_OBYC_GBB_Corrected_0001_VAX_7920.png` | Corrected GBB-VAX assignment to COGS G/L `6010531` |
| 08 | `08_VL01N_Delivery_PGI_Posted.png` | Delivery `80000029` and Material Document `4900000105` |
| 09 | `09_VF01_Billing_Creation_Overview.png` | Billing preview; net `€8,500.00` |
| 10 | `10_VF01_Billing_Document_Saved.png` | Billing Document `90000037` saved |
| 11 | `11_VF03_Display_Billing_Items.png` | Billing document item display |
| 12 | `12_Document_Flow_Post_Billing.png` | SD document flow after billing |
| 13 | `13_FB03_Journal_Entry_9000000001.png` | FI Journal Entry `9000000001` |
| 14 | `14_F28_Bank_GL_Account_Lookup.png` | F-28 Bank G/L `110000` selection |
| 15 | `15_F28_Open_Items_Processing.png` | Customer open-item assignment; difference `€0.00` |
| 16 | `16_F28_Payment_Document_Posted.png` | Payment Document `1000000000` posted |
| 17 | `17_Document_Flow_Fully_Cleared.png` | Final SD document flow in cleared status |
| 18 | `18_FBL5N_Customer_Line_Item_Display.png` | Customer `1000000029` fully cleared; balance `€0.00` |

## P2P — Completed Lifecycle

Target folder: `08-evidence/screenshots/p2p/`

The P2P screenshot set documents the completed procurement chain from Purchase Order through vendor payment and settlement. See `08-evidence/screenshots/p2p/README.md` for the active naming convention.

## Evidence Packs

- `08-evidence/evidence-packs/SAP_O2C_Execution_Report.md`
- `08-evidence/evidence-packs/p2p-lifecycle-report.md`
- `08-evidence/evidence-packs/SAP_SD_FI_Billing_Release_Documentation.md`
- `08-evidence/evidence-packs/SAP_Material_Verification_to_Sales_Order_12.md`

## Evidence Governance

The current core O2C execution uses Material `194`. Older supplied billing evidence using Material `10194` remains preserved only within its separate historical case-study context.