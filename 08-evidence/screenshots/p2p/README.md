# P2P Screenshot Evidence

This folder contains SAP GUI screenshots supporting the complete Procure-to-Pay (P2P) lifecycle.

## Recommended Evidence Sequence

| # | SAP Transaction | Evidence |
|---:|---|---|
| 01 | `ME21N` | Purchase Order `4500000149` |
| 02 | `MIGO` | Goods Receipt / Material Document `5000000062` |
| 03 | `MIRO` | Invoice Verification / Invoice `5105600101` |
| 04 | `MIR4` | FI Accounting Document `5100000000` |
| 05 | `F-53` | Vendor Payment / Payment Document `5000000000` |
| 06 | Vendor Account | Final clearing / zero vendor balance |

## Configuration & Troubleshooting Evidence

Where available, include screenshots showing the issues and their resolutions, such as:

- `MIRO` number-range error and resolution
- `FBN1` number-range configuration
- Posting-period validation
- Tax calculation / Tax Code `A1`
- G/L account `5010032` extension
- GR/IR account `2010621` extension
- `F-53` number-range error and resolution
- Final payment and clearing validation

## Naming Convention

Use a numbered sequence so the evidence follows the business process:

```text
01_ME21N_Purchase_Order.png
02_MIGO_Goods_Receipt.png
03_MIRO_Invoice.png
04_MIR4_FI_Document.png
05_F53_Payment.png
06_Vendor_Clearing.png
```

Additional troubleshooting screenshots should use the same sequence with descriptive names.

## Evidence Rule

Screenshots should represent actual SAP execution evidence. Do not add screenshots that were not captured from the corresponding SAP transaction or supplied as source evidence.
