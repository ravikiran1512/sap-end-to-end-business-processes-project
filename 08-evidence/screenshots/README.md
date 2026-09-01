# SAP Screenshot Evidence

All SAP GUI screenshots belong under `08-evidence/screenshots/`.

## Organization

Screenshots are grouped by business process rather than duplicated by module:

```text
08-evidence/
└── screenshots/
    ├── p2p/
    ├── o2c/
    ├── r2r/
    ├── plan-to-produce/
    ├── service/
    └── enterprise-structure/
```

## Current Evidence

### P2P — Completed

`p2p/` contains the evidence for the completed Procure-to-Pay lifecycle:

`ME21N → MIGO → MIRO → MIR4/FI Verification → F-53 → Vendor Clearing`

### O2C

Future screenshots for the core O2C execution should be stored under `o2c/`. The separate supplied SD-FI billing case should also be kept under the O2C evidence area when its screenshots are available.

## Naming Standard

Use descriptive, numbered filenames that follow the business process:

```text
01_ME21N_Purchase_Order.png
02_MIGO_Goods_Receipt.png
03_MIRO_Invoice.png
04_MIR4_FI_Document.png
05_F53_Payment.png
06_Vendor_Clearing.png
```

Troubleshooting screenshots should use the same process sequence with a concise diagnostic description.

## Evidence Principle

Only actual SAP screenshots or explicitly supplied source evidence should be represented as execution evidence. Documentation must not imply that a screenshot exists when it has not been captured or uploaded.