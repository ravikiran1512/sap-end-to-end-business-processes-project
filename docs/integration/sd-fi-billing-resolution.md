# SD-FI Billing Release & Account Determination Resolution

## Portfolio Case Study

This implementation case study documents the diagnostic and configuration workflow required to release billing document **90000032** from Sales & Distribution (SD) to Financial Accounting (FI) in the TechNova SAP S/4HANA practice environment.

The supplied source document identifies the case as a standard Order-to-Cash flow in which a billing document existed but could not initially be released to FI because multiple downstream prerequisites were incomplete.

## Enterprise Context

| Object | Value |
|---|---|
| Company Code | `9000` — TechNova Mfg. GmbH |
| Sales Organization | `9000` — TechNova Domestic & Export Sales |
| Distribution Channel / Division | `10 / 00` |
| Plant / Storage Location | `9000 / 0001` |
| Chart of Accounts | `BKMG` |
| Fiscal Year / Posting Period | `2026 / 08` |
| Customer / Sold-to / Payer | `1000000021` — Berlin Office Solutions GmbH |
| Billing Document | `90000032` — F2 |
| FI Accounting Document | `9000000000` — RV |
| Material recorded in supplied billing evidence | `10194` — TechNova Business Laptop |
| Invoiced Quantity | `5 EA` |

> **Material governance:** The core O2C project uses **Material 194**. The supplied billing evidence records **10194**. The source identifier is preserved in this case study for evidence traceability and is not presented as the active core-project material master.

## Resolution Sequence

### 1. VF02 — Initial Release Failure

When the release-to-accounting function was executed in `VF02`, billing document `90000032` could not post to FI and returned an account-determination error.

**Root cause:** the SD condition technique could not determine a valid revenue G/L account for the relevant pricing/account-key path. The source case identifies this as the initial integration failure.

### 2. VKOA — Revenue Account Determination

The revenue condition/account-key path was maintained in `VKOA` Table 005:

```text
Application        V
Condition Type     KOFI
Chart of Accounts  BKMG
Sales Organization 9000
Account Key        ERL
G/L Account        6010131
```

**Result:** the revenue determination record was saved successfully.

### 3. OB40 — Output Tax Account Assignment

The next release attempt exposed a tax-account determination issue for table `T030K` and transaction key `MWS`.

The output-tax account assignment was configured as:

```text
Transaction Key    MWS
Chart of Accounts BKMG
G/L Account        2300000
Tax                19% VAT / Tax Code A1
```

**Result:** automatic posting account `2300000` was assigned for MWS.

### 4. FS00 — G/L Master Data for Output Tax

The next release attempt reported that G/L account `2300000` was not defined in chart of accounts `BKMG`.

The account was created/activated in `FS00` for Company Code `9000` with the documented output-tax control settings.

**Result:** G/L `2300000` became available for automatic posting.

### 5. FS00 — G/L Master Data for Sales Revenue

The next release attempt reported that G/L account `6010131` was not defined in Company Code `9000`.

The revenue account was created/extended in `FS00` for Company Code `9000` and saved as the current-revenue account used by the VKOA determination.

**Result:** G/L `6010131` became available for company-code posting.

### 6. FBN1 — FI Document Number Range

After the account-determination and G/L prerequisites were resolved, the release exposed a missing FI document number range:

```text
Object / Company Code  RF_BELEG / 9000
Number Range           Z1
Fiscal Year            2026
From Number            9000000000
To Number              9999999999
Numbering              Internal
```

The source case explains that standard F2 billing creates FI document type `RV`, which uses the configured number-range interval. The interval was added for fiscal year 2026.

**Result:** number-range interval `Z1` was saved.

### 7. VF02 — Successful Release

With revenue determination, tax determination, G/L master data, and FI numbering prerequisites active, the release action in `VF02` succeeded.

**System result:** `Document 90000032 has been saved.`

### 8. FB03 — Financial Verification

The generated accounting document **9000000000** was inspected in `FB03`.

| Line | PK | Account | Description | Tax | Amount (EUR) | Dr/Cr |
|---:|---:|---|---|---|---:|---|
| 1 | `01` | `1000000021` | Berlin Office Solutions GmbH | `A1` | 5,950.00 | Debit |
| 2 | `50` | `6010131` | Current Revenues | `A1` | 5,000.00 | Credit |
| 3 | `50` | `2300000` | Output Tax (19% VAT) | `A1` | 950.00 | Credit |

**Balance:** €5,950.00 debit = €5,950.00 credit.

**Status:** the FI accounting document posted in full balance.

## Business Significance

This case demonstrates that successful SD billing does not by itself guarantee successful FI posting. The billing-to-accounting interface depends on a chain of configuration and master-data prerequisites.

The troubleshooting sequence demonstrates practical implementation capability in:

- Error diagnosis and root-cause isolation
- SD revenue account determination
- Automatic tax account determination
- G/L master-data provisioning
- FI document-number-range configuration
- Cross-module SD-FI validation
- Financial-document verification

## Final O2C / FI Position

The supplied case study establishes the following completed flow:

```text
Sales Order
   ↓
Outbound Delivery
   ↓
Post Goods Issue
   ↓
Billing Document 90000032
   ↓
VF02 Release to Accounting ✓
   ↓
FI Document 9000000000
   ↓
FB03 Balanced Journal Entry ✓
```

The supplied source document states that the O2C process through SD-FI financial posting is fully verified.

## Next Customer Accounting Milestone

The next steps are explicitly documented in the supplied source:

1. **FBL5N** — display the open customer line item for customer `1000000021`, expected at **€5,950.00**.
2. **F-28** — record the incoming customer bank transfer and clear the open invoice line item.

These steps are **planned next execution steps**, not completed evidence in the supplied package.

## Evidence Map

The supplied update contains 18 SAP screenshots covering the initial and intermediate diagnostic/configuration stages. They should be stored under:

`evidence/screenshots/sd/billing-resolution/`

The source PDF is stored as:

`evidence/implementation-evidence-packs/SAP_SD_FI_Billing_Release_Documentation.pdf`

The PDF itself documents the later FBN1, successful VF02 release, and FB03 verification stages. The repository deliberately does not invent standalone SAP screenshots for those stages when the supplied package does not contain them.

## Implementation Learning

The key implementation lesson is the dependency chain: **VKOA → OB40 → FS00 → FBN1 → VF02 → FB03**. Each correction removed a distinct blocker, and the final accounting document provided objective evidence that the SD-FI integration was restored.
