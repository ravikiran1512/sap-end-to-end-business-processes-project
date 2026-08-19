# Controlling (CO)

## Module Introduction

Controlling will establish the management-accounting layer of the TechNova SAP implementation. While Financial Accounting records the company's external financial transactions, CO will be used to understand, monitor, and analyze internal costs and management performance.

This module has **not yet been implemented** in the SAP system. The sections below describe the planned implementation scope and will be replaced or expanded with actual configuration details and SAP evidence as the project progresses.

## What We Plan to Implement

The CO phase will cover the configuration and validation needed to connect internal cost management with the financial foundation already established in FI.

Planned areas include:

- Controlling organizational assignments and relationships with Company Code `9000`
- Cost center structure and master data
- Cost element / G/L account integration where applicable
- Internal cost collection and monitoring
- Internal allocations and assessment/distribution concepts where required
- Planning and comparison of planned versus actual costs
- Relevant profitability and management reporting concepts
- FI/CO integration and financial posting impacts

## Planned Business Perspective

The objective is not simply to create CO master data. We will demonstrate how TechNova can use CO to understand where costs are incurred, which organizational units are responsible for them, and how those costs connect back to FI.

The implementation will therefore be documented from both perspectives:

**Configuration → Business purpose → Transactional use → FI integration → Validation**

## Future Evidence

When CO configuration begins, screenshots will be stored under:

`evidence/screenshots/co/`

Each configuration object will be documented with its relevant fields, assigned values, purpose, validation result, and corresponding SAP evidence.

## Planned Integration

CO will later connect with:

- **FI** — financial accounting and internal cost impacts
- **MM** — procurement and inventory-related cost impacts
- **PP** — production costs and manufacturing activities
- **SD** — sales-related profitability and cost impacts

## Current Status

**Status: Planned**

No CO configuration is being presented as completed until it has actually been executed and validated in the SAP system.
