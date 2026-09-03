# 03 — Business Processes

This section presents the implementation from a business-process perspective rather than by SAP module.

## Process Portfolio

- [Order-to-Cash (O2C)](order-to-cash/README.md)
- [Procure-to-Pay (P2P)](source-to-pay/README.md)
- [Record-to-Report (R2R)](record-to-report/README.md)
- [Plan-to-Produce](plan-to-produce/README.md)
- [Service](service/README.md)

## Current Execution

### Order-to-Cash — Completed

The core O2C lifecycle using Material `194` and Customer `1000000029 — Delta Electronics` is complete:

`VA01 → VL01N → VL02N/PGI → VF01 → FI Posting → F-28 → FBL5N`

Key documents:

- Sales Order: `18`
- Outbound Delivery: `80000029`
- Material Document: `4900000105`
- Billing Document: `90000037`
- FI Journal Entry: `9000000001`
- Incoming Payment: `1000000000`
- Final customer balance: `€0.00`

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