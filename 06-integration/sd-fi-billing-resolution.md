# SD-FI Billing Release & Account Determination Resolution

This case study documents the diagnostic and configuration workflow used to transfer billing document `90000032` from SD to FI, followed by customer open-item verification, incoming payment, and final clearing.

## Diagnostic Chain

`VF02 → VKOA → OB40 → FS00 → FBN1/OBA7 → OBA3 → VF02 → FB03 → FBL5N → F-28 → FBL5N`

## Enterprise Context

- Company Code: `9000`
- Sales Organization: `9000`
- Distribution Channel / Division: `10 / 00`
- Plant / Storage Location: `9000 / 0001`
- Chart of Accounts: `BKMG`
- Fiscal Year / Period: `2026 / 08`
- Customer: `1000000021` — Berlin Office Solutions GmbH
- Material in supplied billing evidence: `10194` — TechNova Business Laptop

## Resolutions

### Revenue — `VKOA`
`ERL → 6010131` for the documented sales context.

### Output Tax — `OB40`
`MWS → 2300000` for Chart of Accounts `BKMG`.

### G/L Master Data — `FS00`
G/L accounts `6010131` (revenue) and `2300000` (output tax) were created/extended for Company Code `9000`.

### FI Number Ranges — `FBN1 / OBA7`
`RV → Z1` (`9000000000–9999999999`) and `DZ → 06` (`6000000000–6999999999`) for fiscal year 2026.

### Customer Tolerance — `OBA3`
Default blank tolerance group for Company Code `9000`, with `€10.00` and `5.0%` payment-difference limits.

## Financial Result

Billing `90000032` generated FI document `9000000000`:

| Account | Amount | Posting |
|---|---:|---|
| Customer `1000000021` | €5,950.00 | Debit |
| Revenue `6010131` | €5,000.00 | Credit |
| Output Tax `2300000` | €950.00 | Credit |

The FI document is balanced at €5,950.00.

## Clearing Result

Payment document `6000000000` (`DZ`) posted on `29.08.2026` for `€5,950.00` and cleared the customer receivable. Final `FBL5N` status: **0 open items; customer balance €0.00**.

## Evidence

Supporting screenshots and evidence packs are maintained under `08-evidence/`. The original detailed source documentation remains preserved in the repository migration history.
