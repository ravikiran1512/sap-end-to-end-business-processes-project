# SAP SD-FI-AR Billing Release & Account Determination — Evidence Summary

## Execution Context

- Company Code: `9000`
- Sales Organization: `9000`
- Chart of Accounts: `BKMG`
- Fiscal Year / Period: `2026 / 08`
- Customer: `1000000021 — Berlin Office Solutions GmbH`
- Billing Document: `90000032` / `F2`
- FI Document: `9000000000` / `RV`
- Incoming Payment: `6000000000` / `DZ`

## Resolution and Clearing Chain

1. `VF02` — initial account-determination failure
2. `VKOA` — revenue condition `ERL` mapped to G/L `6010131`
3. `OB40` — output-tax key `MWS` mapped to G/L `2300000`
4. `FS00` — G/L `2300000` created/validated
5. `FS00` — G/L `6010131` created/validated
6. `FBN1 / OBA7` — FI document-number configuration for fiscal year `2026`
7. `OBA3` — customer tolerance-group configuration
8. `VF02` — billing document released successfully
9. `FB03` — FI document verified as balanced
10. `FBL5N` — customer receivable verified at `€5,950.00`
11. `F-28` — incoming payment `6000000000` posted for `€5,950.00`
12. `FBL5N` — final customer clearing verified; balance `€0.00`

## FBN1 / OBA7 Configuration

| Field | Executed value |
|---|---|
| Company Code | `9000` |
| Object | `RF_BELEG` |
| Billing Document Type | `RV` |
| Number Range | `Z1` |
| Fiscal Year | `2026` |
| From | `9000000000` |
| To | `9999999999` |
| Numbering | Internal |
| Incoming Payment Document Type | `DZ` |
| Incoming Payment Number Range | `06` |
| Payment Range | `6000000000–6999999999` |

## Customer Tolerance

The documented customer tolerance-group configuration for Company Code `9000` permits payment differences up to `€10.00` or `5.0%`.

## Final FI Posting

| Account | Description | Debit | Credit |
|---|---|---:|---:|
| `1000000021` | Berlin Office Solutions GmbH | €5,950.00 | — |
| `6010131` | Current Revenues | — | €5,000.00 |
| `2300000` | Output Tax | — | €950.00 |

**Total:** €5,950.00 debit and €5,950.00 credit.

## Customer Accounting Reconciliation

| Stage | Document | Amount | Result |
|---|---|---:|---|
| Customer receivable | `9000000000` | €5,950.00 | Open item |
| Incoming payment | `6000000000` | €5,950.00 | Received |
| Clearing | `6000000000` | €5,950.00 | Cleared |
| Final customer balance | `FBL5N` | **€0.00** | **Fully cleared** |

## Material Traceability

The core portfolio O2C material is **194 — TechNova Business Laptop**. The supplied billing source records **10194** in its own executed scenario; the source identifier is retained unchanged for evidence traceability.

## Evidence Location

- Screenshot manifest: `evidence/screenshots/SCREENSHOT-MANIFEST.md`
- Billing evidence directory: `evidence/screenshots/sd/billing-resolution/`
- Detailed case study: `docs/integration/sd-fi-billing-resolution.md`

This Markdown file provides a repository-native summary of the supplied billing evidence and the documented completed customer-accounting outcome. It does not claim standalone screenshots for final stages that are not present in the source package.