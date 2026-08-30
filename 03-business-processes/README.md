# 03 — Business Processes

This section presents the implementation from a business-process perspective rather than by SAP module.

## Process Portfolio

- [Order-to-Cash (O2C)](order-to-cash/README.md)
- [Source-to-Pay (S2P)](source-to-pay/README.md)
- [Record-to-Report (R2R)](record-to-report/README.md)
- [Plan-to-Produce (P2P)](plan-to-produce/README.md)
- [Service](service/README.md)

## Current Execution

### Order-to-Cash
Sales Order `12` is established; the next core execution milestone is `VL01N`.

### Source-to-Pay
Purchase Order `4500000149` has reached Goods Receipt through MIGO. Material Document `5000000062` was generated. `MIRO` is next.

The business-process structure is intentionally separated from configuration and evidence so that an interviewer can understand the business flow first and then drill into technical details.
