# SD-FI Billing Release & Account Determination Resolution

## Portfolio Case Study

This implementation evidence package documents the diagnostic and configuration workflow required to release billing document **90000032** from Sales & Distribution (SD) to Financial Accounting (FI) in the TechNova SAP S/4HANA practice environment.

### Scope

`VF02 → VKOA → OB40 → FS00 → FBN1 → VF02 → FB03`

## Executive Outcome

Billing document **90000032** initially could not be released to accounting because several downstream prerequisites were incomplete. The issue was resolved progressively through revenue account determination, tax account assignment, G/L master-data validation, and FI document-number-range configuration.

The final result was a successful VF02 release and generation of FI document **9000000000**, which was verified in `FB03`.

## Resolution Sequence

### 1. VF02 — Initial Release Failure

Billing document **90000032** was saved, but release to accounting was blocked by incomplete account determination.

### 2. VKOA — Revenue Account Determination

The revenue condition/account-key path was maintained as:

`V → KOFI → BKMG → 9000 → ERL → G/L 6010131`

### 3. OB40 — Output Tax Account Assignment

The subsequent release attempt exposed a tax-account determination issue for table `T030K`. Transaction key **MWS** was assigned to **G/L 2300000** in chart of accounts `BKMG`.

### 4. FS00 — G/L Master Data

The required accounts were created/validated for Company Code `9000`:

- **2300000** — Output Tax account
- **6010131** — Current Revenues

### 5. FBN1 — FI Document Number Range

After account determination and G/L master data were corrected, the release exposed a missing FI number-range interval for object `RF_BELEG`.

The executed fix was:

| Field | Value |
|---|---|
| Company Code | `9000` |
| Number Range | `Z1` |
| Fiscal Year | `2026` |
| From Number | `9000000000` |
| To Number | `9999999999` |
| Numbering | Internal |

### 6. VF02 — Successful Release

After all prerequisites were established, billing document **90000032** was released successfully to accounting.

**System result:** `Document 90000032 has been saved.`

### 7. FB03 — Financial Verification

The resulting FI document **9000000000** was opened in `FB03` and verified as a balanced journal entry.

## Final Accounting Result

| Line | PK | Account | Description | Tax | Amount (EUR) | Dr/Cr |
|---:|---:|---|---|---|---:|---|
| 1 | `01` | `1000000021` | Berlin Office Solutions GmbH | `A1` | 5,950.00 | Debit |
| 2 | `50` | `6010131` | Current Revenues | `A1` | 5,000.00 | Credit |
| 3 | `50` | `2300000` | Output Tax (19% VAT) | `A1` | 950.00 | Credit |

**Balance:** €5,950.00 debit = €5,950.00 credit.

## Business Significance

This case demonstrates that SD billing-to-FI posting depends on multiple configuration layers. A billing document may exist successfully while release to accounting remains blocked by missing revenue determination, tax determination, G/L master data, or FI number ranges.

The troubleshooting sequence demonstrates practical SAP implementation capability in:

- Error diagnosis and root-cause isolation
- SD revenue account determination
- Automatic tax account determination
- G/L master-data provisioning
- FI document-number-range configuration
- Cross-module SD-FI validation
- Financial-document verification

## Material Traceability

The **core project O2C workstream uses Material 194 — TechNova Business Laptop**.

The supplied billing evidence package separately records material **10194** in its executed billing scenario. That value is preserved exactly in the source evidence and PDF for traceability rather than being rewritten without system evidence.

## Evidence Map

All billing screenshots are organized under:

`evidence/screenshots/sd/billing-resolution/`

| Screenshot | Evidence |
|---|---|
| `19_vf02_revenue_account_6010131_error.jpg` | Revenue G/L validation in VF02 |
| `20_fs00_gl_6010131_saved.jpg` | Revenue G/L 6010131 saved in FS00 |
| `21_vf02_fi_number_range_z1_error.jpg` | Missing FI number range in VF02 |
| `22_fbn1_number_ranges_before_maintenance.jpg` | FBN1 pre-maintenance state |
| `23_fbn1_z1_2026_saved.jpg` | FBN1 interval Z1 saved for 2026 |
| `24_vf02_successful_release.jpg` | Successful release to accounting |
| `25_fb03_posted_document.jpg` | Final FI document verification |

The complete source evidence document supplied with the update is represented in the repository documentation and evidence manifest.

## Implementation Learning

The important implementation lesson is not only that the invoice was posted, but **why each failure occurred and how the SD-FI integration chain was repaired in dependency order**. This makes the case study suitable as interview evidence for SAP SD/FI integration, troubleshooting, configuration, and end-to-end business-process execution.
