# Financial Accounting (FI)

## My FI Implementation Overview

I am building the Financial Accounting (FI) foundation for **TechNova Manufacturing GmbH** in SAP S/4HANA. I am documenting FI as part of an integrated business-process implementation rather than as isolated transaction practice.

I am using the FI configuration to establish the accounting foundation that I will later connect with Controlling, Materials Management, Sales and Distribution, Production, and end-to-end financial postings.

## 1. FI Organizational Foundation

I am using Company Code **9000** as the financial accounting foundation for TechNova Manufacturing GmbH in Hamburg, Germany.

| Configuration Field | Assigned Value |
|---|---|
| Company Code | **9000** |
| Company Name | TechNova Mfg. GmbH |
| City | Hamburg |
| Country / Region | DE |
| Currency | EUR |
| Language | EN |
| Chart of Accounts | BMKG |
| Fiscal Year Variant | K4 |
| Client | 300 |

I assigned these values to establish the accounting framework in which I will record and validate subsequent financial transactions.

## 2. General Ledger Foundation

I established the initial General Ledger configuration and documented my creation/maintenance of G/L account **1020131**.

### G/L Account 1020131

| Configuration Field | Assigned Value |
|---|---|
| G/L Account | **1020131** |
| Account Description | Receivables |
| German Description | Forderungen |
| Chart of Accounts | BMKG |
| Account Type | S - Balance Sheet Account |
| Account Currency | EUR |
| Field Status Group | G019 |
| Account Group shown during creation | Liquid funds accounts |

I created the account as a balance-sheet G/L account in EUR and maintained it within chart of accounts **BMKG**. I assigned field status group **G019**, which controls which fields are available or required when postings are made to the account.

## 3. Language / Translation Maintenance

I maintained a German translation for the G/L account so that the account description can be represented consistently in the relevant language context.

| Language | Description |
|---|---|
| English | Receivables |
| German | Forderungen |

This means I maintained more than the account number: I also maintained the account master data and its language-dependent description.

## 4. Validation and Configuration Review

During my validation, the account creation process displayed a configuration warning related to the selected account group. My implementation evidence records that **1020131 is intended to represent Receivables**, while the account-group selection displayed **Liquid funds accounts**.

I am intentionally documenting this as a configuration review point rather than presenting it as resolved. Before I use the account in downstream Accounts Receivable or Order-to-Cash processing, I will review and correct the account-group assignment if required by the final design.

This is part of my validation approach: I document both successful configuration steps and findings that require review.

## 5. FI Configuration Management

I associated my FI configuration work with the project's SAP Customizing change-control process.

| Change-Control Field | Value |
|---|---|
| Customizing Request | **A4HK901352** |
| Customizing Task | **A4HK901353** |
| SAP Client | **300** |
| Configuration User | **RAVI** |

I retain this transport information so that my configuration remains traceable to the SAP change-control process.

## 6. Business Purpose

I am establishing the FI foundation so that TechNova can maintain a consistent accounting structure before I execute integrated business scenarios. This foundation will support:

- General Ledger accounting
- Balance-sheet and profit-and-loss reporting
- Receivables-related accounting structures
- Integration with Controlling
- Integration with procurement and inventory accounting
- Integration with sales and billing accounting
- Subsequent financial posting and validation scenarios

## 7. Integration Perspective

I will not configure FI as an isolated module. I will use it as the financial backbone of my end-to-end implementation.

Planned integration includes:

**MM → FI**

I will validate the financial impact created by procurement and inventory transactions.

**SD → FI**

I will validate the financial postings created by sales and billing processes, including receivables-related impacts.

**PP → FI / CO**

I will evaluate the material and cost impacts created by production activity and how they flow into financial and controlling processes.

**FI ↔ CO**

I will connect Financial Accounting and Controlling to support internal cost and profitability analysis.

## 8. Evidence

I maintain FI configuration screenshots separately under:

`evidence/screenshots/fi/`

Recommended evidence naming:

- `gl-account-1020131-receivables.png`
- `gl-account-1020131-control-data.png`
- `gl-account-1020131-bank-interest.png`
- `gl-account-1020131-translation.png`
- `gl-account-1020131-save-warning.png`

## 9. Current FI Status

**Status: In Progress**

I have documented the initial FI organizational and General Ledger foundation. I will add further FI configuration, integration, posting scenarios, validation, and end-to-end testing only after I perform them in the SAP system and capture supporting implementation evidence.

> **Documentation principle:** This section records what I actually configured and validated in the project. Future FI activities will be added only after I perform them in SAP and support them with implementation evidence.
