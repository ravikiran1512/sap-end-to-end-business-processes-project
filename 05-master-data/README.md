# 05 — Master Data

## Active Core Material

**Material `194` — TechNova Business Laptop** is the active core project material.

## Customer Master

The O2C billing case uses customer `1000000021` — Berlin Office Solutions GmbH.

## Procurement Master Data

The completed P2P lifecycle uses:

| Business Object | Value |
|---|---|
| Vendor | `12026` — Apex Industrial Supplies |
| Purchase Order | `4500000149` |
| Material | TechNova 15.6" Display Panel |
| Quantity | `10 EA` |
| Unit Price | `€50.00` |
| Net Value | `€500.00` |
| Cost Center | `CC9000` |
| Profit Center | `PC9000` |
| Target Expense G/L | `5010032` |
| GR/IR G/L | `2010621` |

Vendor `12026` became the Accounts Payable business partner for the completed procurement transaction. MIRO created a payable of `€595.00`, which was subsequently cleared through F-53.

Master-data documentation is organized by business object so downstream processes can reference a single source of truth.
