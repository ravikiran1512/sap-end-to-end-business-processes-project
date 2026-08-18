# SAP Configuration Register

This directory is the **detailed configuration register** for the TechNova Manufacturing GmbH SAP S/4HANA implementation.

The register records the values actually assigned, verified, or explicitly documented during the project. It distinguishes executed configuration from existing/verified system entries so that pre-existing demo/server objects are not presented as TechNova-created objects.

> **Documentation rule:** Do not infer a field value merely because the field exists on an SAP screen. A value is recorded here only when it is explicitly supported by the project evidence or configuration summary.

## 1. Project / System Context

| Field | Assigned / Confirmed Value | Status |
|---|---|---|
| Project | TechNova End-to-End SAP Implementation | Confirmed |
| Company | TechNova Manufacturing GmbH | Confirmed |
| Company Code | `9000` | Completed |
| Location | Hamburg, Germany | Confirmed |
| Country / Region | `DE` | Confirmed |
| Currency | `EUR` | Confirmed |
| Language Key | `EN` | Confirmed |
| SAP Client | `300` | Project documentation |
| Configuration User | `RAVI` | Evidence/documentation |
| Customizing Request | `A4HK901352` | Confirmed |
| Customizing Task | `A4HK901353` | Confirmed |

## 2. Company Code — Detailed Fields

| SAP Field | Assigned Value | Status |
|---|---|---|
| Company Code | `9000` | Completed |
| Company Name | `TechNova Mfg. GmbH` | Completed |
| City | `Hamburg` | Completed |
| Country / Region | `DE` | Completed |
| Currency | `EUR` | Completed |
| Language Key | `EN` | Completed |
| Chart of Accounts | `BMKG` | Completed / documented |
| Fiscal Year Variant | `K4` | Completed / documented |

The SAP GUI evidence shows these company-code parameters on the Company Code Global Data screen. Other fields visible on the screen are **not recorded as configured unless explicitly populated/documented**.

## 3. Enterprise Structure

### Plant

| Field | Value | Status |
|---|---|---|
| Plant | `TN01` | Completed |
| Description | TechNova Manufacturing Plant | Completed |
| Company Code Assignment | `9000` | Confirmed project structure |

### Storage Location

| Field | Value | Status |
|---|---|---|
| Storage Location | `RM10` | Completed & verified |
| Description | Raw materials | Confirmed |
| Plant | `TN01` | Confirmed |

### Purchasing Organization

| Field / Assignment | Value | Status |
|---|---|---|
| Purchasing Organization | `TN01` | Created |
| Description | TechNova Purchasing | Created |
| Assigned Company Code | `9000` | Completed |
| Assigned Plant | `TN01` | Completed |
| Default / Standard Purchasing Organization | `TN01` → `TN01` plant | Completed |
| Reference Purchasing Organization | `TN01` | Completed |

### Sales Organization

| Field / Assignment | Value | Status |
|---|---|---|
| Sales Organization | `TN01` | Created |
| Assigned Company Code | `9000` | Completed |
| Distribution Channel | `10` | Existing system entry used / assigned |
| Distribution Channel Description | B2C (Online) | Confirmed |
| Division | `00` | Existing system entry used / assigned |
| Division Description | Product Division 00 | Confirmed |
| Sales Area | `TN01 / 10 / 00` | Created / confirmed |

## 4. FI — G/L Account Master Data

### G/L Account 1020131 — Receivables

| SAP Field | Executed Value | Status |
|---|---|---|
| G/L Account | `1020131` | Created |
| Company Code | `9000` | Assigned |
| Description | `Receivables` | Assigned |
| German Text | `Forderungen` | Assigned |
| G/L Account Type | Balance Sheet Account | Assigned |
| Field Status Group | `G019` — Other receivables/payables | Assigned |
| Account Currency | `EUR` | Assigned |
| Chart of Accounts | `BMKG` | Used |

### Translation

| Language | Short Text | Long Text |
|---|---|---|
| English | Receivables | Receivables |
| German | Forderungen | Forderungen |

### Save Validation

SAP displayed the warning:

> `Keep balance sheet accounts in local currency only.`

The warning did not block saving and the account was subsequently saved successfully.

### Configuration Review Item

The execution evidence shows the account group **Liquid funds accounts** selected for G/L account `1020131`, while the business description is **Receivables**. This is recorded as an open configuration-review item and must be validated before the account is used in downstream Accounts Receivable / Order-to-Cash processing.

## 5. Transport / Change Control

| Field | Value |
|---|---|
| Customizing Request | `A4HK901352` |
| Customizing Task | `A4HK901353` |
| Configuration User | `RAVI` |
| Project Description | TechNova Manufacturing – SAP End-to-End Implementation |

## 6. Configuration Status Legend

- **Created / Completed** — explicitly executed during the project.
- **Verified** — existing object checked and confirmed for project use.
- **Existing system entry used** — pre-existing object used; not presented as newly created.
- **Review** — configuration exists but requires validation before downstream use.
- **TODO** — not yet configured.
- **TBD** — TechNova-specific value has not yet been confirmed.

## 7. Evidence Links

Screenshots are maintained separately under:

`evidence/screenshots/enterprise-structure/`

`evidence/screenshots/fi/`

`evidence/screenshots/mm/`

`evidence/screenshots/sd/`

`evidence/screenshots/co/`

`evidence/screenshots/pp/`

`evidence/screenshots/service/`

`evidence/screenshots/integration/`

`evidence/screenshots/testing/`

## 8. Next Configuration Register Expansion

As each module is implemented, add the **complete set of assigned fields**, not only the headline configuration object. Each entry should capture:

1. SAP configuration object
2. Field name
3. Exact assigned value
4. Whether the object was created, verified, or pre-existing
5. Transport/change reference
6. Screenshot evidence
7. Validation result
8. Downstream integration impact

This register will become the detailed configuration audit trail for the final SAP portfolio case study.
