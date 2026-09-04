# SAP Screenshot Manifest

This manifest indexes the current process-oriented screenshot evidence stored under `08-evidence/screenshots/`.

## Plan-to-Produce — Manufacturing Execution

Target folder: `08-evidence/screenshots/plan-to-produce/`

| # | Screenshot | SAP Evidence |
|---:|---|---|
| 01 | `01_OPK4_Confirmation_Parameters_Saved.png` | Confirmation parameters saved for Plant `TN01` / Order Type `PP01` |
| 02 | `02_CO15_Enter_Actual_Data_Confirmation.png` | Production confirmation header and quantities |
| 03 | `03_CO15_Order_Confirmation_Saved.png` | Production Order `1000020` confirmation saved |
| 04 | `04_MIGO_Goods_Receipt_Order_Initial.png` | Initial MIGO Goods Receipt for production order |
| 05 | `05_MIGO_Error_Account_Determination_GBB_AUF.png` | Missing `BKMG / GBB / 0001 / AUF / 7920` account determination |
| 06 | `06_OBYC_GBB_AUF_Account_Not_Created.png` | Initial OBYC account assignment issue |
| 07 | `07_OBYC_Chart_of_Accounts_Search_Hitlist.png` | Chart of Accounts `BKMG` account search |
| 08 | `08_OBYC_Assign_Account_6010531.png` | Initial GBB-AUF assignment to G/L `6010531` |
| 09 | `09_MIGO_Error_Cost_Element_Category_KI280.png` | `KI280` Cost Element Category error |
| 10 | `10_FS00_Change_GL_Account_Centrally.png` | Central G/L review for `6010531` |
| 11 | `11_OBYC_GBB_AUF_Assign_Account_5010032.png` | GBB-AUF reassigned to G/L `5010032` |
| 12 | `12_MIGO_Document_Check_OK.png` | MIGO validation returned `Document is O.K.` |
| 13 | `13_MIGO_Error_Table_TFBEFU_CR_Missing.png` | Missing production GR valuation variant dependency |
| 14 | `14_OPK9_Maintain_Goods_Receipt_Valuation.png` | `OPK9` assignment `TN01 → 001` |
| 15 | `15_OPK9_Data_Saved.png` | Valuation configuration saved |
| 16 | `16_MIGO_Goods_Receipt_Posted_5000000063.png` | Goods Receipt posted; Material Document `5000000063` |
| 17 | `17_MMBE_Stock_Overview_Verification.png` | `95 EA` unrestricted stock confirmed in `FG10` |
| 18 | `18_CO03_Production_Order_Header_Final_Status.png` | Final production-order status and quantities |

## O2C — Core Lifecycle

Target folder: `08-evidence/screenshots/o2c/`

The O2C screenshot set documents the completed chain from PGI troubleshooting through billing, FI posting, incoming payment, and final customer clearing. See `08-evidence/screenshots/o2c/README.md` for the active naming convention.

## P2P — Completed Lifecycle

Target folder: `08-evidence/screenshots/p2p/`

The P2P screenshot set documents the completed procurement chain from Purchase Order through vendor payment and settlement. See `08-evidence/screenshots/p2p/README.md` for the active naming convention.

## Evidence Packs

- `08-evidence/evidence-packs/SAP_Plan_to_Produce_Execution_Report.md`
- `08-evidence/evidence-packs/SAP_O2C_Execution_Report.md`
- `08-evidence/evidence-packs/p2p-lifecycle-report.md`
- `08-evidence/evidence-packs/SAP_SD_FI_Billing_Release_Documentation.md`
- `08-evidence/evidence-packs/SAP_Material_Verification_to_Sales_Order_12.md`

## Evidence Governance

The current core manufacturing and O2C scenarios use Material `194`. Older supplied billing evidence using Material `10194` remains preserved only within its separate historical case-study context.