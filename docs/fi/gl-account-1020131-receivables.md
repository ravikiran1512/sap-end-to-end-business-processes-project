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

## Evidence sequence

1. **Page 5** — Create G/L Account Centrally; account 1020131 and Receivables description are visible.
2. **Page 6** — Control Data shows EUR as account currency; Create/bank/interest evidence shows field status group G019 and the required selection used during execution.
3. **Page 7** — Key word / translation evidence shows English `Receivables` and German `Forderungen`.
4. **Page 8** — SAP save warning states that balance-sheet accounts should be kept in local currency only and confirms that the account could still be saved.

## Configuration review item

The source evidence explicitly records that the execution screenshot shows the account group **Liquid funds accounts** selected for account 1020131. Because the business meaning is **Receivables**, this assignment must be reviewed and validated before the account is used in downstream Accounts Receivable or Order-to-Cash transactions.

This repository records the executed state and does not silently reinterpret or change it.

## Source

`TechNova SAP End-to-End Implementation Evidence Pack`, current project evidence, pages 5–8.
