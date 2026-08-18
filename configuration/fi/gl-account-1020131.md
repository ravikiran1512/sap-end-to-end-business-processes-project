# FI Configuration — G/L Account 1020131

## Business Object

**G/L Account:** `1020131`  
**Business Meaning:** Receivables  
**Company Code:** `9000`  
**Chart of Accounts:** `BMKG`

## Account Master Data

| Field | Executed Value |
|---|---|
| G/L Account | `1020131` |
| Company Code | `9000` |
| Description | Receivables |
| German Text | Forderungen |
| G/L Account Type | Balance Sheet Account |
| Field Status Group | `G019` — Other receivables/payables |
| Account Currency | `EUR` |
| Chart of Accounts | `BMKG` |

## Language / Translation

| Language | Short Text | Long Text |
|---|---|---|
| English | Receivables | Receivables |
| German | Forderungen | Forderungen |

## Save Validation

During save, SAP displayed the warning:

`Keep balance sheet accounts in local currency only.`

The warning was non-blocking and the account was saved successfully.

## Configuration Review Item

The execution screenshot shows **Liquid funds accounts** selected as the account group while the account business meaning is **Receivables**. This is retained exactly as executed and must be reviewed before downstream Accounts Receivable / Order-to-Cash use.

## Evidence

Place the corresponding screenshots in:

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
