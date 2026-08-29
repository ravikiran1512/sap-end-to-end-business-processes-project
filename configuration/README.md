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

## 3. FI — Existing G/L Documentation

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

## 4. MM — Current Material Master

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

## 5. SD — Shipping Point Determination

| Field | Value |
|---|---|
| Shipping Condition | `01` |
| Loading Group | `0002` |
| Plant | `0001` |
| Shipping Point | `0001` |

This combination was added/saved for the executed practice scenario after SAP initially could not determine a shipping point.

## 6. SD-FI-AR Billing Resolution Configuration

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

## 7. Material Traceability

The **core project material identifier is 194**.

The supplied billing-resolution evidence records material **10194**. That source value is retained exactly inside the billing evidence for auditability and is not used as the active core O2C material identifier.

## 8. Status Legend

- **Created / Completed** — explicitly executed.
- **Verified** — existing object checked and confirmed for project use.
- **Case-study scope** — supplied as part of the billing-resolution implementation context.
- **Existing system entry used** — pre-existing object used in the scenario.
- **Review** — configuration exists but requires validation.
- **TODO** — not yet configured.
- **TBD** — project-specific value not yet confirmed.

## 9. Evidence

Screenshots are organized under:

- `evidence/screenshots/mm/`
- `evidence/screenshots/sd/`
- `evidence/screenshots/sd/billing-resolution/`
- `evidence/screenshots/fi/`
- `evidence/screenshots/integration/`

The configuration register is expanded as new SAP milestones are executed and validated.

## 10. Current Configuration Status

**SD-FI-AR billing case: Completed through customer clearing.**

**Core O2C execution: In Progress — Sales Order `12` remains at the pre-delivery milestone, with `VL01N` as the next operational step.**