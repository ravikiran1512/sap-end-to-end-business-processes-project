# Financial Accounting (FI)

## FI Implementation Overview

The Financial Accounting (FI) work in this project establishes the accounting foundation required for TechNova Manufacturing GmbH to record and report its business transactions in SAP S/4HANA.

The implementation is being documented as a business-process configuration rather than as isolated transaction practice. The configuration connects the organizational structure with the General Ledger and prepares the environment for later integration with Controlling, Materials Management, Sales and Distribution, Production, and end-to-end financial postings.

## 1. FI Organizational Foundation

The FI configuration is built around Company Code **9000**, representing TechNova Manufacturing GmbH in Hamburg, Germany.

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

The Company Code is the central organizational unit used for external accounting. Its assigned currency, country, language, chart of accounts, and fiscal year variant provide the accounting framework in which financial transactions will subsequently be recorded.

## 2. General Ledger Foundation

The project established the initial General Ledger configuration and documented the creation/maintenance of G/L account **1020131**.

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

The account was created as a balance-sheet G/L account in EUR and maintained within chart of accounts **BMKG**. The field status group **G019** controls which fields are available or required when postings are made to the account.

## 3. Language / Translation Maintenance

The G/L account was also maintained with a German translation so that the account description can be represented consistently in the relevant language context.

| Language | Description |
|---|---|
| English | Receivables |
| German | Forderungen |

This demonstrates that the configuration was not limited to entering the account number; the account master data and its language-dependent description were also maintained.

## 4. Validation and Configuration Review

During validation, the account creation process displayed a configuration warning related to the selected account group. The implementation evidence records that **1020131 is intended to represent Receivables**, while the account-group selection displayed **Liquid funds accounts**.

This item is intentionally documented as a configuration review point rather than silently treated as correct. Before the account is used in downstream Accounts Receivable or Order-to-Cash processing, the account-group assignment should be reviewed and corrected if required by the final design.

This is part of the project's validation approach: configuration evidence records both successful entries and findings that require review.

## 5. FI Configuration Management

The FI configuration work is associated with the project's SAP Customizing change-control process.

| Change-Control Field | Value |
|---|---|
| Customizing Request | **A4HK901352** |
| Customizing Task | **A4HK901353** |
| SAP Client | **300** |
| Configuration User | **RAVI** |

The transport information is retained so that the configuration remains traceable to the SAP change-control process.

## 6. Business Purpose

The FI foundation enables TechNova to establish a consistent accounting structure before executing integrated business scenarios. The configuration provides the basis for:

- General Ledger accounting
- Balance-sheet and profit-and-loss reporting
- Receivables-related accounting structures
- Integration with Controlling
- Integration with procurement and inventory accounting
- Integration with sales and billing accounting
- Subsequent financial posting and validation scenarios

## 7. Integration Perspective

FI will not be configured as an isolated module. The configuration will become the financial backbone of the end-to-end implementation.

Planned integration includes:

**MM → FI**

Procurement and inventory transactions will generate relevant accounting impacts.

**SD → FI**

Sales and billing processes will ultimately create financial postings and receivables-related impacts.

**PP → FI / CO**

Production activity will create material and cost impacts that feed the financial and controlling processes.

**FI ↔ CO**

Financial accounting and controlling will work together to support internal cost and profitability analysis.

## 8. Evidence

Screenshots for FI configuration are maintained separately under:

`evidence/screenshots/fi/`

Recommended evidence naming:

- `gl-account-1020131-receivables.png`
- `gl-account-1020131-control-data.png`
- `gl-account-1020131-bank-interest.png`
- `gl-account-1020131-translation.png`
- `gl-account-1020131-save-warning.png`

## 9. Current FI Status

**Status: In Progress**

The initial FI organizational and General Ledger foundation has been documented. Further FI configuration, integration, posting scenarios, validation, and end-to-end testing will be added as the implementation progresses.

> **Documentation principle:** This section records what was actually configured and validated in the project. Future FI activities will be added only after they are performed in the SAP system and supported by implementation evidence.
