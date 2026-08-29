# SAP S/4HANA Order-to-Cash (O2C) End-to-End Implementation & Execution Case Study

## Executive Summary

This case study documents the end-to-end **Order-to-Cash (O2C)** business cycle executed for **TechNova Mfg. GmbH**, Company Code `9000`. The scenario connects master data and enterprise structure with transactional execution, logistics processing, billing, SD-FI account determination, financial posting, incoming payment, and customer-account clearing.

The implementation is documented as a business-process case study rather than a collection of isolated SAP transactions. Each phase records the relevant business object, SAP transaction, configuration dependency, execution result, and financial impact.

> **Material traceability:** The supplied billing scenario identifies the material as **`10194 — TechNova Business Laptop`**. That identifier is retained exactly in this case study as part of the executed evidence. The broader repository also contains the core project material revision **`194`**; the two identifiers are not silently merged.

---

## Phase 1 — Master Data & Enterprise Structure Foundation

The O2C scenario operates within the following documented enterprise and master-data context:

| Object | Value | Business Role |
|---|---|---|
| Company Code | `9000` — TechNova Mfg. GmbH | Financial accounting entity |
| Sales Organization | `9000` — Domestic & Export Sales | Sales responsibility |
| Distribution Channel | `10` | Distribution route |
| Division | `00` | Product/business division |
| Plant | `9000` | Logistics/operational location |
| Storage Location | `0001` | Inventory storage subdivision |
| Chart of Accounts | `BKMG` | Accounting structure used by the billing case |
| Fiscal Year / Posting Period | `2026 / 08` | Financial posting context |
| Customer / Sold-to / Payer | `1000000021` — Berlin Office Solutions GmbH | Customer accounting and sales relationship |
| Material | `10194` — TechNova Business Laptop | Product sold in the billing case |
| Base Unit | `EA` | Inventory and sales unit |
| Invoiced Quantity | `5 EA` | Billing quantity |

The organizational structure provides the context required to connect sales processing, logistics execution, billing, and Financial Accounting.

---

## Phase 2 — Transactional Execution Roadmap

The complete case follows this business sequence:

```text
Customer Requirement
        ↓
Sales Order
        ↓
Outbound Delivery
        ↓
Goods Issue
        ↓
Billing Document
        ↓
SD → FI Account Determination
        ↓
Accounting Document
        ↓
Customer Open Item
        ↓
Incoming Payment
        ↓
Customer Account Clearing
        ↓
Zero Open Balance
```

### 1. Sales Order Creation — `VA01`

- **Order Type:** `OR` — Standard Order
- **Material:** `10194 — TechNova Business Laptop`
- **Order Quantity:** `5 EA`
- **Net Price:** `1,000.00 EUR / EA`
- **Net Order Value:** `5,000.00 EUR`
- **Output VAT:** `950.00 EUR` at 19%
- **Gross Order Value:** `5,950.00 EUR`

The sales order establishes the commercial demand that drives the downstream logistics and billing process.

### 2. Outbound Delivery — `VL01N`

The outbound delivery is created with reference to the sales order.

- **Shipping Point:** `9000`
- **Reference:** Sales Order `12` where applicable to the executed O2C chain

The delivery document controls the logistics execution of the confirmed customer requirement.

### 3. Goods Issue — `VL02N`

Post Goods Issue completes the physical logistics handover represented by the delivery.

- **Movement Type:** `601` — Goods Issue for Delivery
- **Storage Location:** `0001`
- **Quantity:** `5 EA`

**Operational impact:** the goods issue reduces the available inventory and records the corresponding inventory movement in SAP.

### 4. Billing Document — `VF01`

The billing document is generated with reference to the completed logistics process.

- **Billing Type:** `F2` — Standard Invoice
- **Billing Document:** `90000032`
- **Net Value:** `5,000.00 EUR`
- **Output VAT:** `950.00 EUR`
- **Gross Value:** `5,950.00 EUR`

At this stage, the commercial transaction has been converted into a customer receivable and is ready for transfer to Financial Accounting, subject to successful account determination and FI prerequisites.

---

## Phase 3 — SD-FI Integration Diagnostics & Defect Resolution

The initial attempt to release billing document `90000032` to Financial Accounting exposed a sequence of configuration and master-data dependencies. The issues were resolved systematically rather than bypassed.

### 1. Revenue Account Determination — `VKOA`

**Issue:** No valid revenue G/L account was available for the relevant SD condition/account-key combination.

**Configuration resolution:**

```text
Application         V
Condition Type      KOFI
Chart of Accounts   BKMG
Sales Organization  9000
Account Key         ERL
Revenue G/L         6010131
```

**Result:** the SD revenue account determination path was established.

### 2. Output Tax Account Determination — `OB40`

**Issue:** Automatic posting for transaction key `MWS` could not determine the required tax G/L account.

**Configuration resolution:**

```text
Transaction Key     MWS
Chart of Accounts   BKMG
G/L Account         2300000
Tax                 19% VAT / Tax Code A1
```

**Result:** output-tax account `2300000` was assigned for automatic posting.

### 3. G/L Master Data — `FS00`

The required G/L accounts were established and extended for Company Code `9000`:

| G/L Account | Description | Accounting Role |
|---|---|---|
| `2300000` | Output Tax | Balance Sheet / Tax Payable |
| `6010131` | Current Revenues | Profit & Loss / Sales Revenue |

The configuration supplied for the case identifies `2300000` with tax category `>` and field status group `G001`, while revenue account `6010131` uses tax category `*`.

**Result:** both accounts became available for the required billing-related financial postings.

### 4. FI Document Number Ranges — `FBN1` / `OBA7`

**Issue:** Required FI document-number intervals were not available for the relevant document types.

**Resolution:**

| Document Type | Number Range | Fiscal Year | Interval |
|---|---|---:|---|
| `RV` — Billing Accounting Document | `Z1` | 2026 | `9000000000–9999999999` |
| `DZ` — Incoming Payment | `06` | 2026 | `6000000000–6999999999` |

The document-type and number-range relationship was configured so that billing and incoming-payment documents could be assigned valid FI document numbers.

### 5. Customer Tolerance Group — `OBA3`

**Issue:** No tolerance-group entry was available in table `T043G` for Company Code `9000`.

**Resolution:** A default blank tolerance group was established for Company Code `9000` with the documented payment-difference limits:

- **Amount tolerance:** `10.00 EUR`
- **Percentage tolerance:** `5.0%`

**Result:** the customer-account clearing process received the required tolerance configuration.

---

## Phase 4 — Successful Billing Release & Financial Verification

### 1. Billing Release — `VF02`

After the revenue account, tax account, G/L master data, FI number ranges, and customer tolerance prerequisites were resolved, billing document `90000032` was successfully released to Financial Accounting.

**System result:** billing document `90000032` was saved and transferred to FI.

### 2. Accounting Document — `FB03`

The generated FI accounting document is:

- **Document:** `9000000000`
- **Document Type:** `RV`
- **Company Code:** `9000`

| Posting Key | Account | Description | Amount (EUR) | Debit / Credit |
|---:|---|---|---:|---|
| `01` | `1000000021` | Berlin Office Solutions GmbH — Customer Receivable | `5,950.00` | Debit |
| `50` | `6010131` | Current Revenues | `5,000.00` | Credit |
| `50` | `2300000` | Output Tax — 19% VAT | `950.00` | Credit |

**Reconciliation:**

`Debit €5,950.00 = Credit €5,950.00`

The accounting document is therefore balanced and represents the financial impact of the billed customer transaction.

---

## Phase 5 — Incoming Payment & Customer Clearing

### 1. Customer Open Item — `FBL5N`

Following successful billing-to-FI integration, the customer receivable is available as an open item for customer `1000000021`.

- **Customer:** `1000000021 — Berlin Office Solutions GmbH`
- **Open Receivable:** `5,950.00 EUR`
- **Source Accounting Document:** `9000000000`

The open-item view provides the control point for the subsequent cash-collection transaction.

### 2. Incoming Payment — `F-28`

The customer payment is recorded against the outstanding receivable.

- **Payment Document:** `6000000000`
- **Document Type:** `DZ`
- **Posting Date:** `29.08.2026`
- **Bank Account:** `110000`
- **Payment Amount:** `5,950.00 EUR`
- **Customer Account:** `1000000021`

The incoming payment clears the customer receivable generated by the billing transaction.

### 3. Final Clearing Verification — `FBL5N`

The final customer-account review confirms that the receivable and incoming payment have been linked through clearing document `6000000000`.

**Final status:**

- Open customer items: **0**
- Cleared invoice: `9000000000`
- Cleared payment: `6000000000`
- Final customer balance: **`0.00 EUR`**

The O2C cycle is therefore complete from commercial demand through cash collection and customer-account clearing.

---

## End-to-End Process Result

```text
VA01 — Sales Order
        ↓
VL01N — Outbound Delivery
        ↓
VL02N — Post Goods Issue
        ↓
VF01 — Billing Document 90000032
        ↓
VF02 — Release to Accounting
        ↓
VKOA — Revenue Determination
        ↓
OB40 — Tax Account Determination
        ↓
FS00 — G/L Master Data
        ↓
FBN1 / OBA7 — FI Number Ranges
        ↓
FB03 — Accounting Document 9000000000
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

## Financial Reconciliation

| Stage | Document | Financial Position |
|---|---|---:|
| Billing | `90000032` | €5,950.00 gross receivable |
| FI Posting | `9000000000` | €5,950.00 debit / €5,950.00 credit |
| Incoming Payment | `6000000000` | €5,950.00 received |
| Final Customer Balance | `FBL5N` | **€0.00** |

This reconciliation demonstrates the complete financial lifecycle of the O2C transaction: **revenue recognition → tax liability → customer receivable → cash receipt → customer clearing**.

---

## Business & Implementation Significance

This case study demonstrates practical SAP implementation capability across both transactional execution and integration troubleshooting.

### SAP Capabilities Demonstrated

- Enterprise-structure understanding
- Sales-order processing
- Logistics execution
- Goods issue and inventory impact
- Billing execution
- SD revenue account determination
- Automatic tax account determination
- G/L master-data configuration
- FI document-number-range configuration
- Customer tolerance-group configuration
- SD-FI integration troubleshooting
- Accounting-document validation
- Customer open-item management
- Incoming-payment processing
- Customer-account clearing
- End-to-end financial reconciliation

### Key Implementation Lesson

The case demonstrates that an O2C process can progress successfully through sales and billing while still failing at the SD-FI integration boundary. Resolving the issue requires tracing the dependency chain from **account determination → tax determination → G/L master data → document numbering → customer accounting**.

The final reconciliation closes the loop by demonstrating that the billed amount was posted correctly, collected in full, and cleared from the customer account.

---

## Evidence & Repository Organization

The O2C case-study artifacts are maintained within the existing repository structure:

```text
process-flows/
└── order-to-cash/
    └── README.md

docs/
├── sd/
├── fi/
└── integration/

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

The repository should distinguish between **completed execution evidence** and **documentation derived from the supplied case study**. No SAP screenshot should be presented as captured evidence unless the corresponding screenshot is actually available.

---

## Status

**Status: End-to-End O2C case study documented through customer clearing.**

The documented business flow now extends from sales-order creation through logistics execution, billing, SD-FI integration, financial posting, incoming payment, and final customer-account clearing.