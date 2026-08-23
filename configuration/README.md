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

## 5. MM — Material Master

### Material 184 — TechNova Business Laptop

| SAP Field / View | Value | Status |
|---|---|---|
| Material | `184` | Created |
| Description | `TechNova Business Laptop` | Assigned |
| Material Type | `Finished Product` | Assigned |
| Industry | `Mechanical engineering` | Selected during creation |
| Base Unit | `EA – Each` | Assigned |
| Gross Weight | `2 KG` | Maintained |
| Net Weight | `1.700 KG` | Maintained |
| Dimensions | `35 × 24 × 2 cm` | Maintained/documented |
| Plant | `0001 – AN PLANT – BENGALURU` | Extended |
| Sales Organization | `0001 – Sales Org. 001` | Extended |
| Distribution Channel | `01 – Distribution Channel 01` | Extended |
| Classification | Class Type `001` / Class `1000` | Assigned |
| Tax Classification | `1 – Full tax` for displayed entries | Maintained |
| Availability Check | `02 – Individual requirements` | Maintained |
| Profit Center | `PC0001` | Assigned |
| Inventory Planning Mode | `eSPP calculation` | Displayed/reviewed |
| Extended SPP Planning Scenario | None selected | Reviewed |
| International Trade Export fields | Blank in captured workflow | Reviewed |
| Sales Text | No text maintained | Reviewed |
| Material Group | Valid system entry selected | Mandatory validation resolved; exact code not preserved |
| Creation Result | `Material 184 created` | **Success** |

### Material Master Implementation Notes

I created the material as a finished product so that it can later participate in sales, procurement, inventory, planning, logistics, and accounting processes. I selected the relevant material views because different business functions consume different parts of the material master.

I used SAP value help for the Material Group rather than inventing a code manually. The system displayed a catalogue of 185 material groups, but the captured evidence does not preserve the exact selected code, so the register intentionally does not guess it.

I also reviewed the Item Category Group value help in Sales Organization 2 but did not record a final Item Category Group because the evidence does not establish one as assigned.

The detailed implementation record is maintained at:

`docs/mm/material-184-tech-nova-business-laptop.md`

## 6. Transport / Change Control

| Field | Value |
|---|---|
| Customizing Request | `A4HK901352` |
| Customizing Task | `A4HK901353` |
| Configuration User | `RAVI` |
| Project Description | TechNova Manufacturing – SAP End-to-End Implementation |

## 7. Configuration Status Legend

- **Created / Completed** — explicitly executed during the project.
- **Verified** — existing object checked and confirmed for project use.
- **Existing system entry used** — pre-existing object used; not presented as newly created.
- **Review** — configuration exists but requires validation before downstream use.
- **TODO** — not yet configured.
- **TBD** — TechNova-specific value has not yet been confirmed.

## 8. Evidence Links

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

## 9. Next Configuration Register Expansion

As each module is implemented, I will add the **complete set of assigned fields**, not only the headline configuration object. Each entry should capture:

1. SAP configuration object
2. Field name
3. Exact assigned value
4. Whether the object was created, verified, or pre-existing
5. Transport/change reference
6. Screenshot evidence
7. Validation result
8. Downstream integration impact

This register will become the detailed configuration audit trail for my final SAP portfolio case study.
