# SD-FI Billing Release & Account Determination Resolution

## Portfolio Case Study

This implementation evidence package documents the diagnostic and configuration workflow required to release billing document **90000032** from SD to Financial Accounting in the TechNova SAP S/4HANA practice environment.

### Scope

**VF02 → VKOA → OB40 → FS00 → FBN1 → VF02 → FB03**

## Executive Outcome

The billing document initially failed during release to accounting because SAP could not resolve required revenue, tax, G/L master-data, and FI document-number-range prerequisites. The configuration was progressively corrected and the invoice was ultimately released successfully, generating FI document **9000000000**.

## Resolution Sequence

### 1. VF02 — Initial Release Failure

Billing document **90000032** was saved but could not be released to accounting because account determination was incomplete.

### 2. VKOA — Revenue Account Determination

The executed configuration maintained the revenue condition/account-key path:

`V` → `KOFI` → `BKMG` → `9000` → `ERL` → **G/L `6010131`**

### 3. OB40 — Output Tax Account Assignment

The next release attempt exposed a tax-account determination issue for table T030K. Transaction key **MWS** was assigned to **G/L `2300000`** in chart of accounts `BKMG`.

### 4. FS00 — G/L Master Data

The required G/L accounts were created/validated for Company Code `9000`:

- **2300000** — output-tax account
- **6010131** — revenue account

### 5. FBN1 — FI Document Number Range

The release then exposed a missing FI number-range interval for object `RF_BELEG`.

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

After the prerequisites were established, billing document **90000032** was successfully released to accounting.

### 7. FB03 — Financial Verification

The resulting FI document **9000000000** was inspected in `FB03`.

## Final Accounting Result

| Line | PK | Account | Description | Tax | Amount (EUR) | Dr/Cr |
|---:|---:|---|---|---|---:|---|
| 1 | `01` | `1000000021` | Berlin Office Solutions GmbH | `A1` | 5,950.00 | Debit |
| 2 | `50` | `6010131` | Current Revenues | `A1` | 5,000.00 | Credit |
| 3 | `50` | `2300000` | Output Tax (19% VAT) | `A1` | 950.00 | Credit |

**Balance:** €5,950.00 debit = €5,950.00 credit.

## Business Significance

This case demonstrates that SD billing-to-FI posting is dependent on multiple configuration layers. A billing document can exist successfully while release to accounting remains blocked by missing account determination, G/L master data, or FI number ranges.

The troubleshooting sequence demonstrates practical SAP implementation skills in:

- Error diagnosis and root-cause isolation
- SD revenue account determination
- Automatic tax account determination
- G/L master-data provisioning
- FI document-number-range configuration
- Cross-module SD-FI validation
- Financial-document verification

## Material Traceability Note

The supplied billing evidence identifies material **10194**. The main project master-data milestone has separately been revised from **184** to **194**. This billing artifact therefore retains **10194 exactly as executed** and does not reinterpret the source evidence.

## Evidence

Standalone screenshots are stored under:

`evidence/screenshots/sd/billing-resolution/`

The complete supplied evidence document is:

`evidence/implementation-evidence-packs/SAP_SD_FI_Billing_Release_Documentation.pdf`

The final standalone screenshots `19` and `20` are extracted from the supplied PDF for direct repository navigation.
