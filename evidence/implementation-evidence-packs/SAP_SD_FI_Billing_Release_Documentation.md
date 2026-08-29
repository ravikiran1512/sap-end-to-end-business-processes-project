# SAP SD-FI Billing Release & Account Determination — Evidence Summary

## Execution Context

- Company Code: `9000`
- Sales Organization: `9000`
- Chart of Accounts: `BKMG`
- Fiscal Year / Period: `2026 / 08`
- Customer: `1000000021 — Berlin Office Solutions GmbH`
- Billing Document: `90000032` / `F2`
- Final FI Document: `9000000000` / `RV`

## Resolution Chain

1. `VF02` — initial account-determination failure
2. `VKOA` — revenue condition `ERL` mapped to G/L `6010131`
3. `OB40` — output-tax key `MWS` mapped to G/L `2300000`
4. `FS00` — G/L `2300000` created/validated
5. `FS00` — G/L `6010131` created/validated
6. `FBN1` — number range `Z1` created for fiscal year `2026`
7. `VF02` — billing document released successfully
8. `FB03` — FI document verified as balanced

## FBN1 Configuration

| Field | Executed value |
|---|---|
| Company Code | `9000` |
| Object | `RF_BELEG` |
| Number Range | `Z1` |
| Fiscal Year | `2026` |
| From | `9000000000` |
| To | `9999999999` |
| Numbering | Internal |

## Final FI Posting

| Account | Description | Debit | Credit |
|---|---|---:|---:|
| `1000000021` | Berlin Office Solutions GmbH | €5,950.00 | — |
| `6010131` | Current Revenues | — | €5,000.00 |
| `2300000` | Output Tax | — | €950.00 |

**Total:** €5,950.00 debit and €5,950.00 credit.

## Material Traceability

The core portfolio O2C material is **194 — TechNova Business Laptop**. The supplied billing source records **10194** in its own executed scenario; the source identifier is retained unchanged for evidence traceability.

## Evidence Location

- Screenshot manifest: `evidence/screenshots/SCREENSHOT-MANIFEST.md`
- Billing evidence directory: `evidence/screenshots/sd/billing-resolution/`
- Detailed case study: `docs/integration/sd-fi-billing-resolution.md`

This Markdown file provides a repository-native text summary of the supplied PDF evidence so the implementation logic remains searchable and reviewable in GitHub.
