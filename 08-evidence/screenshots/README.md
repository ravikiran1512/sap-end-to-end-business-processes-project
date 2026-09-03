# SAP Screenshot Evidence

All SAP GUI screenshots belong under `08-evidence/screenshots/`.

## Organization

Screenshots are grouped by business process rather than duplicated by module:

```text
08-evidence/
└── screenshots/
    ├── o2c/
    ├── p2p/
    ├── r2r/
    ├── plan-to-produce/
    ├── service/
    └── enterprise-structure/
```

## Current Evidence

### O2C — Completed

`o2c/` is the dedicated location for the current core O2C execution using Material `194` and Customer `1000000029`.

The supplied package contains 18 screenshots covering:

`MMPV period error/resolution → OBYC account determination → Delivery/PGI → VF01 Billing → FI Journal Entry → F-28 Payment → Cleared Document Flow → FBL5N zero balance`

See [`o2c/README.md`](o2c/README.md) for the complete filename sequence.

### P2P — Completed

`p2p/` contains the evidence for the completed Procure-to-Pay lifecycle:

`ME21N → MIGO → MIRO → MIR4/FI Verification → F-53 → Vendor Clearing`

See [`p2p/README.md`](p2p/README.md) for the active naming convention.

## Naming Standard

Use descriptive, numbered filenames that follow the business-process chronology. Troubleshooting screenshots should remain in the same process folder so that error, correction, retest, and final result can be followed sequentially.

## Evidence Principle

Only actual SAP screenshots or explicitly supplied source evidence should be represented as execution evidence. Documentation must not imply that a screenshot exists when it has not been captured or uploaded.