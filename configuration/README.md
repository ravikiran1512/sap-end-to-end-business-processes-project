# SAP Configuration Register

This directory is the detailed configuration register for the TechNova Manufacturing GmbH SAP S/4HANA implementation.

The register records values actually assigned, verified, or explicitly documented during the project. It distinguishes executed configuration from existing system entries so that practice/demo objects are not presented as newly created TechNova objects.

> **Documentation rule:** Record a field only when the project evidence supports it. Do not infer undocumented values.

## 1. Project / System Context

| Field | Value | Status |
|---|---|---|
| Project | TechNova End-to-End SAP Implementation | Confirmed |
| Company | TechNova Manufacturing GmbH | Confirmed |
| Company Code | `9000` | Completed |
| Location | Hamburg, Germany | Confirmed |
| Country / Region | `DE` | Confirmed |
| Currency | `EUR` | Confirmed |
| Language | `EN` | Confirmed |
| SAP Client | `300` | Project documentation |
| Configuration User | `RAVI` | Evidence/documentation |
| Customizing Request | `A4HK901352` | Confirmed |
| Customizing Task | `A4HK901353` | Confirmed |

## 2. Enterprise Structure

| Object | Value | Status |
|---|---|---|
| Company Code | `9000` | Completed |
| Sales Organization | `9000` | Completed / case-study scope |
| Distribution Channel | `10` | Case-study scope |
| Division | `00` | Case-study scope |
| Plant | `9000` | Case-study scope |
| Storage Location | `0001` | Case-study scope |
| Chart of Accounts | `BKMG` | Case-study scope |
| Fiscal Year / Period | `2026 / 08` | Case-study scope |
| Customer / Sold-to / Payer | `1000000021` | Case-study scope |

## 3. CO / Universal Journal Integration

| Configuration / Process | Value | Status |
|---|---|---|
| Controlling Area | `9000` | Executed |
| CO Version | `0` | Executed |
| Leading Ledger | `0L` | Assigned to CO Version `0` |
| Configuration Table | `FINSC_CMP_VERSNC` | Updated |
| Consistency Check | `FINS_CUST_CONS_CHK` | Blocking version/ledger error cleared |
| Mass Data Project | `PRJ_9000` | Executed |
| Activity | `B2K` | Successfully completed |
| Posting Simulation | `FINS_CUST_CONS_CHK_P` | Posting block resolved |
| Processing Result | `0` errors / `0` warnings | Completed |

### CO Integration Milestone

The executed configuration aligns CO Area `9000`, Version `0`, and Leading Ledger `0L`. Mass Data Project `PRJ_9000` / Activity `B2K` was subsequently completed to remove the posting restriction associated with the incomplete journal-entry update.

Detailed documentation: `docs/co/README.md`

## 4. FI — Existing G/L Documentation

| Field | Value | Status |
|---|---|---|
| G/L Account | `1020131` | Created |
| Company Code | `9000` | Assigned |
| Description | Receivables | Assigned |
| German Text | Forderungen | Assigned |
| Account Type | Balance Sheet Account | Assigned |
| Field Status Group | `G019` | Assigned |
| Currency | `EUR` | Assigned |
| Chart of Accounts | `BMKG` | Existing documentation |

**Review item:** The earlier evidence shows the account group **Liquid funds accounts** while the business description is Receivables. This remains a configuration-review item before downstream Accounts Receivable use. The separate O2C billing case uses chart of accounts `BKMG`; these two documented contexts are not silently merged.

## 5. MM — Current Material Master

### Material 194 — TechNova Business Laptop

| SAP Field / View | Value | Status |
|---|---|---|
| Material | `194` | Active project material |
| Description | `TechNova Business Laptop` | Assigned |
| Material Type | `Finished Product` | Assigned |
| Industry | `Mechanical engineering` | Selected during creation |
| Base Unit | `EA – Each` | Assigned |
| Gross Weight | `2 KG` | Maintained/documented |
| Net Weight | `1.700 KG` | Maintained/documented |
| Dimensions | `35 × 24 × 2 cm` | Maintained/documented |
| Plant | `0001 – AN PLANT – BENGALURU` | Extended |
| Sales Organization | `0001 – Sales Org. 001` | Extended |
| Distribution Channel | `01 – Distribution Channel 01` | Extended |
| Classification | Class Type `001` / Class `1000` | Assigned |
| Tax Classification | `1 – Full tax` | Maintained |
| Availability Check | `02 – Individual requirements` | Maintained |
| Profit Center | `PC0001` | Assigned |
| Inventory Planning Mode | `eSPP calculation` | Reviewed |
| Loading Group | `0002 – Forklift` | Maintained |
| Transportation Group | `0004 – Parcel` | Maintained |
| Material Group | Valid SAP entry selected | Exact code not preserved |

Detailed material documentation: `docs/mm/material-194-tech-nova-business-laptop.md`

## 6. MM — Inbound Procurement & Goods Receipt

| Field | Value | Status |
|---|---|---|
| Purchase Order | `4500000149` | Executed scenario |
| Vendor | Apex Industrial Supplies GmbH | Executed scenario |
| Material | TechNova 15.6" Display Panel | Executed scenario |
| Quantity | `10 EA` | Executed |
| Cost Center | `CC9000` | Documented |
| Profit Center | `PC9000` | Documented |
| Target G/L | `5010032` | Documented |
| Transaction | `MIGO` | Executed |
| Operation | `A01` Goods Receipt | Executed |
| Reference | `R01` Purchase Order | Executed |
| Movement Type | `101` | Executed |
| Material Document | `5000000062` | Posted successfully |
| Posting Date | `30.08.2026` | Confirmed |
| Downstream Process | `MIRO` → FI → `F-53` | Completed |
| Vendor Clearing | `€0.00` | Completed |

The Goods Receipt was successfully posted after the CO/Universal Journal posting prerequisite was resolved. The complete P2P case subsequently covered MIRO invoice verification, FI verification, F-53 payment, and vendor clearing.

## 7. PP — Plan-to-Produce / Manufacturing Configuration

| Configuration / Process | Value | Status |
|---|---|---|
| Production Order | `1000020` | Executed |
| Order Type | `PP01` | Executed |
| Material | `194 — TechNova Business Laptop` | Executed |
| Plant | `TN01` | Executed |
| Storage Location | `FG10` | Executed |
| Confirmation Parameters | `OPK4` | Configured |
| Production Confirmation | `CO15` | `10 EA` confirmed |
| Goods Receipt | `MIGO` / Movement `101` | Posted |
| Material Document | `5000000063` | Generated |
| Inventory Verification | `MMBE` | `95 EA` unrestricted |
| Production Order Review | `CO03` | `REL / CNF / PDLV` validated |
| GBB-AUF Account Determination | `OBYC` / Valuation Class `7920` | Resolved |
| CO Cost Element Compatibility | `KI280` | Resolved |
| GR Valuation Variant | `OPK9` / `TN01` → `001` | Configured |

Detailed manufacturing documentation: `03-business-processes/plan-to-produce/README.md`

## 8. SD — Shipping Point Determination

| Field | Value |
|---|---|
| Shipping Condition | `01` |
| Loading Group | `0002` |
| Plant | `0001` |
| Shipping Point | `0001` |

This combination was added/saved for the executed practice scenario after SAP initially could not determine a shipping point.

## 9. SD-FI-AR Billing Resolution Configuration

| Area | Transaction | Executed / documented result |
|---|---|---|
| Revenue account determination | `VKOA` | `ERL` → G/L `6010131` for `BKMG` / Sales Org `9000` |
| Output tax account determination | `OB40` | `MWS` → G/L `2300000` |
| G/L master data | `FS00` | G/L `2300000` and `6010131` established/validated |
| FI number ranges | `FBN1 / OBA7` | `RV → Z1`, `DZ → 06`, fiscal year `2026` |
| Customer tolerance | `OBA3` | Default tolerance group; `€10.00` / `5.0%` limits |
| Billing release | `VF02` | Successful for billing document `90000032` |
| Accounting verification | `FB03` | FI document `9000000000` verified and balanced |
| Customer open item | `FBL5N` | `€5,950.00` receivable documented |
| Incoming payment | `F-28` | Payment document `6000000000`, `€5,950.00` |
| Final clearing | `FBL5N` | Customer balance `€0.00` |

Detailed case study: `docs/integration/sd-fi-billing-resolution.md`

## 10. Material Traceability

The **core project material identifier is 194**.

The supplied historical billing-resolution evidence records material **10194**. That source value is retained exactly inside the historical billing evidence for auditability and is not used as the active core project material identifier.

## 11. Status Legend

- **Created / Completed** — explicitly executed.
- **Verified** — existing object checked and confirmed for project use.
- **Case-study scope** — supplied as part of the billing-resolution implementation context.
- **Existing system entry used** — pre-existing object used in the scenario.
- **Review** — configuration exists but requires validation.
- **TODO** — not yet configured.
- **TBD** — project-specific value not yet confirmed.

## 12. Evidence

Current evidence is organized under the consolidated structure:

- `08-evidence/evidence-packs/`
- `08-evidence/screenshots/o2c/`
- `08-evidence/screenshots/p2p/`
- `08-evidence/screenshots/plan-to-produce/`

## 13. Current Configuration Status

**CO / Universal Journal:** Completed for the executed configuration scope.

**MM / P2P:** Completed through MIRO, FI verification, F-53 payment, and vendor clearing.

**O2C:** Completed through delivery, PGI, billing, FI posting, incoming payment, and customer clearing for the current core scenario.

**Plan-to-Produce:** Completed through production confirmation, finished-goods receipt, inventory verification, and production-order validation.

**R2R:** In Progress — production-order period-end activities `TECO`, `KKS2`, and `KO88` remain for the next phase.

**Service:** Planned — execution not yet started.
