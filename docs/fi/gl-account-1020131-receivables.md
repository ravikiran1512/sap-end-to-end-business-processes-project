# G/L Account 1020131 — Receivables

## Business purpose

A G/L account was created for TechNova company code 9000 to represent Receivables.

## Executed master-data values

| Field | Value |
|---|---|
| G/L Account | **1020131** |
| Company Code | **9000** |
| Description | **Receivables** |
| German text | **Forderungen** |
| G/L Account Type | Balance Sheet Account |
| Field Status Group | **G019 — Other receivables/payables** |
| Account Currency | **EUR** |
| Chart of Accounts | BMKG |

## Configuration and validation

The G/L account was maintained in the SAP system with its organizational assignment, account description, account type, currency, chart of accounts, and field status settings. The account description was also maintained in English and German.

During validation, SAP displayed a non-blocking warning concerning the currency treatment of balance-sheet accounts. The account could still be saved successfully.

## Language / translation

| Language | Description |
|---|---|
| English | `Receivables` |
| German | `Forderungen` |

## Configuration review item

The execution evidence shows **Liquid funds accounts** selected as the account group while the business meaning of G/L account `1020131` is **Receivables**. This configuration point is intentionally retained as executed and must be reviewed and validated before the account is used in downstream Accounts Receivable or Order-to-Cash processes.

The repository documents the actual implementation state rather than silently changing or reinterpreting the configuration.

## Evidence

Corresponding screenshots are maintained under:

`evidence/screenshots/fi/`

Recommended filenames:

- `gl-account-1020131-receivables.png`
- `gl-account-1020131-control-data.png`
- `gl-account-1020131-bank-interest.png`
- `gl-account-1020131-translation.png`
- `gl-account-1020131-save-warning.png`

## Change Control

- Customizing Request: `A4HK901352`
- Customizing Task: `A4HK901353`
- Configuration User: `RAVI`

## Source

`TechNova SAP End-to-End Implementation Evidence Pack`, current project evidence.