# 03 — Business Processes

This section presents the implementation from a business-process perspective rather than by SAP module.

## Process Portfolio

- [Order-to-Cash (O2C)](order-to-cash/README.md)
- [Procure-to-Pay (P2P)](source-to-pay/README.md)
- [Record-to-Report (R2R)](record-to-report/README.md)
- [Plan-to-Produce](plan-to-produce/README.md)
- [Service](service/README.md)

## Current Execution

### Order-to-Cash
Sales Order `12` is established; the next core execution milestone is `VL01N`.

### Procure-to-Pay — Completed

The procurement lifecycle for PO `4500000149` is complete:

`ME21N → MIGO → MIRO → MIR4/FI verification → F-53 → vendor clearing`

Key documents:

- Purchase Order: `4500000149`
- Material Document: `5000000062`
- Logistics Invoice: `5105600101`
- FI Invoice Document: `5100000000`
- Payment Document: `5000000000`
- Final vendor payable balance: `€0.00`

The business-process structure is intentionally separated from configuration and evidence so that an interviewer can understand the business flow first and then drill into technical details.
