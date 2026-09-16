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

### Plan-to-Produce / Manufacturing — Completed

The manufacturing case now covers both production execution and the documented CO-PC period-end close:

`Production Order 1000020 → OPK4 → CO15 → MIGO 101 → Material Document 5000000063 → MMBE → CO03 → CO02/TECO + SETC → KKS2 → CO_ABRECHN → OBYC/PRD → OKB9 → KO88 → KKBC_ORD → FB03`

Key results:

- Material: `194 — TechNova Business Laptop`
- Plant / Storage Location: `TN01 / FG10`
- Production Order: `1000020` (`PP01`)
- Confirmed Yield: `10 EA`
- Goods Receipt Material Document: `5000000063`
- Final unrestricted stock: `95 EA`
- Period-end settlement period: `09/2026`
- Settlement document: FI `1000000001` / `SA`
- Remaining production-order balance after settlement: `€0.00`

Troubleshooting resolved during the manufacturing and close lifecycle:

- `OBYC` GBB-AUF account determination for Valuation Class `7920`
- `KI280` cost-element category compatibility
- `OPK9` valuation variant assignment `TN01 → 001`
- `KD522` settlement number range assignment in `CO_ABRECHN`
- `M8147` `OBYC/PRD` account determination
- `KI235` default CO assignment through `OKB9`

The manufacturing case is complete through production execution, finished-goods receipt, inventory reconciliation, period-end settlement, order-balance verification, and FI posting verification.

Detailed period-end case: [Period-End Controlling Close](plan-to-produce/period-end-controlling-close.md)

The business-process structure is intentionally separated from configuration and evidence so that an interviewer can understand the business flow first and then drill into technical details.