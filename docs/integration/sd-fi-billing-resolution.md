# SD-FI Billing Release & Account Determination Resolution

## Portfolio Case Study

This case study documents the diagnostic and configuration workflow used to transfer billing document **90000032** from Sales and Distribution (SD) to Financial Accounting (FI) in the TechNova SAP S/4HANA practice environment, followed by customer open-item verification, incoming payment, and final clearing.

The scenario demonstrates an important O2C integration principle: successful billing does not automatically guarantee successful FI posting. Revenue determination, tax account determination, G/L master data, document numbering, and customer-account configuration must all be available before the financial document can be posted and cleared.

> **Material traceability:** The supplied billing scenario records **`10194 — TechNova Business Laptop`**. This identifier is preserved exactly for evidence traceability. The broader repository also contains the core project material revision **`194`**; these identifiers are not silently merged.

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
| Material recorded in billing evidence | `10194` — TechNova Business Laptop |
| Invoiced Quantity | `5 EA` |
| Billing Document | `90000032` — F2 |
| FI Accounting Document | `9000000000` — RV |
| Incoming Payment Document | `6000000000` — DZ |

---

## Diagnostic & Resolution Sequence

### 1. `VF02` — Initial Billing Release Failure

The initial release of billing document `90000032` to Financial Accounting returned an account-determination error.

**Root cause:** the SD condition technique could not determine a valid revenue G/L account for the relevant pricing/account-key path.

**Resolution path:** trace the SD pricing/account-key combination into revenue account determination rather than bypassing the accounting interface.

### 2. `VKOA` — Revenue Account Determination

The required revenue determination record was maintained in Table `005`:

```text
Application          V
Condition Type       KOFI
Chart of Accounts    BKMG
Sales Organization   9000
Account Key          ERL
Revenue G/L Account  6010131
```

**Result:** the `ERL` revenue account determination was established for the documented sales context.

### 3. `OB40` — Output Tax Account Determination

The next billing-release attempt exposed a missing automatic posting assignment for transaction key `MWS` in table `T030K`.

The documented configuration was:

```text
Transaction Key     MWS
Chart of Accounts   BKMG
G/L Account         2300000
Tax                 19% VAT / Tax Code A1
```

**Result:** output-tax account `2300000` was assigned for automatic tax posting.

### 4. `FS00` — Output Tax G/L Master Data

The tax-account determination required G/L account `2300000` to exist in the relevant accounting structure.

The account was created/extended in `FS00` for Company Code `9000` with the documented output-tax control settings.

**Result:** G/L `2300000` became available for automatic tax posting.

### 5. `FS00` — Revenue G/L Master Data

The subsequent release attempt identified G/L account `6010131` as unavailable for Company Code `9000`.

The revenue account was created/extended in `FS00` and established as the current-revenue account used by the `VKOA` determination.

**Result:** G/L `6010131` became available for company-code posting.

### 6. `FBN1` / `OBA7` — FI Document Number Ranges

The next release attempt exposed missing FI document-number prerequisites.

The documented configuration is:

| Document Type | Number Range | Fiscal Year | Interval |
|---|---|---:|---|
| `RV` — Billing Accounting Document | `Z1` | 2026 | `9000000000–9999999999` |
| `DZ` — Incoming Payment | `06` | 2026 | `6000000000–6999999999` |

The document-type and number-range relationship was configured so that both billing and incoming-payment documents could receive valid FI document numbers.

### 7. `OBA3` — Customer Tolerance Group

The customer-accounting process also required a tolerance-group entry in table `T043G` for Company Code `9000`.

A default blank tolerance group was configured with:

- Amount tolerance: **`10.00 EUR`**
- Percentage tolerance: **`5.0%`**

**Result:** the required tolerance configuration was available for customer payment processing and clearing.

### 8. `VF02` — Successful Release to Accounting

After the revenue determination, tax account assignment, G/L master data, FI number ranges, and customer-account prerequisites were resolved, billing document `90000032` was successfully released to Financial Accounting.

**Result:** the billing transaction generated FI accounting document `9000000000`.

---

## Financial Accounting Verification — `FB03`

The generated accounting document is:

- **Document:** `9000000000`
- **Document Type:** `RV`
- **Company Code:** `9000`

| Posting Key | Account | Description | Tax | Amount (EUR) | Debit / Credit |
|---:|---|---|---|---:|---|
| `01` | `1000000021` | Berlin Office Solutions GmbH — Customer Receivable | `A1` | `5,950.00` | Debit |
| `50` | `6010131` | Current Revenues | `A1` | `5,000.00` | Credit |
| `50` | `2300000` | Output Tax — 19% VAT | `A1` | `950.00` | Credit |

### Accounting Reconciliation

**Debit:** €5,950.00  
**Credit:** €5,950.00  
**Difference:** €0.00

The accounting document is balanced and represents the financial impact of the customer billing transaction.

---

## Customer Accounting & Clearing

### 1. `FBL5N` — Open Customer Item

The posted receivable is reviewed in `FBL5N` for customer `1000000021`.

- Customer: `1000000021 — Berlin Office Solutions GmbH`
- Open receivable: **€5,950.00**
- Source accounting document: `9000000000`

This establishes the outstanding customer balance created by the billing transaction.

### 2. `F-28` — Incoming Payment

The customer payment is recorded against the outstanding receivable.

| Field | Value |
|---|---|
| Payment Document | `6000000000` |
| Document Type | `DZ` |
| Posting Date | `29.08.2026` |
| Bank Account | `110000` |
| Payment Amount | `€5,950.00` |
| Customer Account | `1000000021` |

The incoming payment matches the outstanding customer receivable in full.

### 3. `FBL5N` — Final Clearing Verification

The final customer-account review confirms that the invoice and incoming payment are linked through clearing document `6000000000`.

**Final reconciliation:**

| Item | Result |
|---|---:|
| Invoice / Receivable | €5,950.00 |
| Incoming Payment | €5,950.00 |
| Remaining Open Items | **0** |
| Final Customer Balance | **€0.00** |

The customer account is fully cleared.

---

## End-to-End SD-FI / AR Flow

```text
Customer Requirement
        ↓
Sales Order
        ↓
Outbound Delivery
        ↓
Post Goods Issue
        ↓
Billing Document 90000032
        ↓
VF02 — Release to Accounting
        ↓
VKOA — Revenue Account Determination
        ↓
OB40 — Output Tax Account Determination
        ↓
FS00 — G/L Master Data
        ↓
FBN1 / OBA7 — FI Number Ranges
        ↓
FB03 — FI Document 9000000000
        ↓
FBL5N — Customer Open Item
        ↓
F-28 — Incoming Payment 6000000000
        ↓
FBL5N — Final Clearing Verification
        ↓
Customer Balance = €0.00
```

---

## Business Significance

The case demonstrates how an SAP implementation consultant approaches a cross-module O2C issue: identify the first integration error, trace the underlying dependency, configure the missing prerequisite, retest, and continue until the complete business outcome is validated.

The scenario demonstrates practical capability in:

- O2C business-process execution
- SD billing and accounting integration
- Revenue account determination
- Automatic tax account determination
- G/L master-data provisioning
- FI document-number-range configuration
- Customer tolerance-group configuration
- Error diagnosis and root-cause isolation
- Accounting-document validation
- Customer open-item management
- Incoming-payment processing
- Customer-account clearing
- End-to-end financial reconciliation

### Key Implementation Lesson

The critical dependency chain is:

**VKOA → OB40 → FS00 → FBN1/OBA7 → VF02 → FB03 → FBL5N → F-28 → FBL5N**

Resolving each dependency transformed an initially blocked billing-to-accounting interface into a fully reconciled customer transaction. The final state confirms that the revenue and tax postings were balanced, the customer payment was received in full, and the customer account was cleared to zero.

---

## Evidence & Repository Organization

The case-study documentation is maintained within the existing SAP portfolio repository:

```text
process-flows/
└── order-to-cash/
    └── README.md

docs/
├── sd/
├── fi/
└── integration/
    └── sd-fi-billing-resolution.md

evidence/
├── screenshots/
│   ├── sd/
│   ├── fi/
│   └── integration/
└── implementation-evidence-packs/
```

Recommended O2C evidence naming:

```text
01_Sales_Order_VA01.png
02_Outbound_Delivery_VL01N.png
03_Goods_Issue_VL02N.png
04_Billing_Document_VF01.png
05_Accounting_Document_FB03.png
06_Open_Items_FBL5N.png
07_Incoming_Payment_F-28.png
08_Cleared_Items_FBL5N.png
O2C_Case_Study_TechNova.pdf
```

Evidence must distinguish between actual SAP screenshots and documentation derived from the supplied case-study source. No screenshot should be presented as captured SAP evidence unless the corresponding image is available in the repository.

## Status

**End-to-End O2C case study documented through customer-account clearing.**

The documented lifecycle now covers commercial demand, logistics execution, billing, SD-FI integration, financial posting, customer open-item management, incoming payment, and final clearing.