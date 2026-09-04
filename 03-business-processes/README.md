# 03 — Business Processes

This section presents the implementation from a business-process perspective rather than by SAP module.

## Process Portfolio

- [Order-to-Cash (O2C)](order-to-cash/README.md)
- [Procure-to-Pay (P2P)](source-to-pay/README.md)
- [Record-to-Report (R2R)](record-to-report/README.md)
- [Plan-to-Produce / Manufacturing](plan-to-produce/README.md)
- [Service](service/README.md)

## Current Execution

### Order-to-Cash — Completed

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

`ME21N → MIGO → MIRO → MIR4/FI verification → F-53 → vendor clearing`

Key documents:

- Purchase Order: `4500000149`
- Material Document: `5000000062`
- Logistics Invoice: `5105600101`
- FI Invoice Document: `5100000000`
- Payment Document: `5000000000`
- Final vendor payable balance: `€0.00`

### Plan-to-Produce / Manufacturing — Completed Through Finished-Goods Receipt

`Production Order 1000020 → OPK4 → CO15 → MIGO 101 → Material Document 5000000063 → MMBE → CO03`

Key results:

- Material: `194 — TechNova Business Laptop`
- Plant / Storage Location: `TN01 / FG10`
- Production Order: `1000020` (`PP01`)
- Confirmed Yield: `10 EA`
- Goods Receipt Material Document: `5000000063`
- Final unrestricted stock: `95 EA`
- Final order status includes `REL`, `CNF`, `PDLV`

Troubleshooting resolved during the manufacturing cycle:

- `OBYC` GBB-AUF account determination for Valuation Class `7920`
- `KI280` cost-element category issue
- `OPK9` valuation variant assignment `TN01 → 001`

The manufacturing execution cycle is complete through confirmation, finished-goods receipt, inventory reconciliation, and final production-order validation. Technical completion, variance calculation, and settlement remain part of the next period-end/R2R phase.

The business-process structure is intentionally separated from configuration and evidence so that an interviewer can understand the business flow first and then drill into technical details.