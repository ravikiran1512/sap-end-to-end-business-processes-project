# Implementation Evidence Packs

I store versioned evidence packs here as the project grows.

## Current Evidence Pack — 24 August 2026

### Material Verification → Sales Order 12

Source document supplied for this milestone:

`SAP_Material_Verification_to_Sales_Order_12(1).pdf`

The evidence covers:

- MM03 verification of Material `184`
- MM02 Loading Group `0002 — Forklift`
- MM02 Transportation Group `0004 — Parcel`
- Shipping Point Determination: `01 / 0002 / 0001 → 0001`
- VA01 Standard Sales Order `12`
- Incompletion handling for missing Net Value
- PR00 pricing at `1.00 EUR / EA`
- Final net value `10.00 EUR`
- Customer `1000000020 — TechNova GmbH`
- Customer reference `TECHNOVA-001`

The corresponding implementation narrative is maintained in:

`docs/sd/material-verification-to-sales-order-12.md`

The screenshot mapping is maintained in:

`evidence/screenshots/SCREENSHOT-MANIFEST.md`

## Repository Binary-File Note

The PDF supplied in the current working session has been used as the source for the repository documentation. The current GitHub connector available to me can create and update UTF-8 text files, but it does not provide a binary-file upload operation for the PDF or JPG/PNG evidence files.

I therefore keep the exact intended repository path and filename documented here rather than pretending that the binary PDF has been uploaded when it has not.

When I have a binary upload-capable Git workflow available, the PDF should be placed at:

`evidence/implementation-evidence-packs/SAP_Material_Verification_to_Sales_Order_12.pdf`

The screenshots should be placed under their corresponding module folders documented in `evidence/screenshots/SCREENSHOT-MANIFEST.md`.

## Naming Convention

For future packs I use:

`TechNova_SAP_Implementation_Evidence_Pack_vX.pdf`

Each version should document the SAP milestones covered and identify any configuration items that still require review.
