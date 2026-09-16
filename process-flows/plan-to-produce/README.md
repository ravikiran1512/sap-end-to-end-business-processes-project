# Plan-to-Produce — Manufacturing Workflow

## Current Execution Status

**Completed — production execution through manufacturing CO-PC period-end settlement and FI verification.**

The executed TechNova scenario uses Production Order `1000020` for Material `194 — TechNova Business Laptop` at Plant `TN01` / Storage Location `FG10`.

## End-to-End Flow

```text
Production Order 1000020
        ↓
OPK4 — Confirmation Parameters
        ↓
CO15 — Production Confirmation / 10 EA Yield
        ↓
MIGO — Goods Receipt / Movement 101
        ↓
Material Document 5000000063
        ↓
MMBE — 95 EA Unrestricted Stock
        ↓
CO03 — Final Order Validation
        ↓
CO02 / TECO + SETC
        ↓
KKS2 — Variance Assessment
        ↓
CO_ABRECHN — Settlement Number Range
        ↓
OBYC / PRD — Account Determination
        ↓
OKB9 — Default CO Assignment
        ↓
KO88 — Actual Settlement
        ↓
KKBC_ORD — Order Balance €0.00
        ↓
FB03 — FI Document 1000000001
```

## Integration Flow

```text
PP Production Order
        ↓
CO Confirmation / Actual Costs
        ↓
MIGO Goods Receipt
        ↓
MM Inventory
        ↓
CO-PC Period-End Close
        ↓
KO88 Settlement
        ↓
FI Journal Entry 1000000001
```

## Period-End Close

The documented Period `09/2026` close resolved and validated:

- `KV 017` during `KKS2` variance assessment
- `KD522` settlement number-range assignment in `CO_ABRECHN`
- `M8147` `OBYC / PRD` account determination
- `KI235` default CO assignment through `OKB9`
- `KO88` actual settlement
- `KKBC_ORD` remaining order balance of `€0.00`
- `FB03` FI settlement document `1000000001`

## Troubleshooting Covered

- `OBYC` GBB-AUF account determination for Valuation Class `7920`.
- `KI280` cost-element compatibility and the documented G/L correction to `5010032`.
- `OPK9` valuation variant assignment for Valuation Area `TN01` → Valuation Variant `001`.
- `CO_ABRECHN` settlement number-range assignment for Controlling Area `9000`.
- `OBYC / PRD` account determination for Chart of Accounts `BKMG`.
- `OKB9` default Cost Center assignment `CC9000` for Cost Element `5010032`.

## Evidence

- Detailed execution case: [`03-business-processes/plan-to-produce/README.md`](../../03-business-processes/plan-to-produce/README.md)
- Period-end close: [`03-business-processes/plan-to-produce/period-end-controlling-close.md`](../../03-business-processes/plan-to-produce/period-end-controlling-close.md)
- Evidence pack: [`08-evidence/evidence-packs/SAP_Plan_to_Produce_Execution_Report.md`](../../08-evidence/evidence-packs/SAP_Plan_to_Produce_Execution_Report.md)
- Screenshots: `08-evidence/screenshots/plan-to-produce/`

## Next Phase

The manufacturing CO-PC period-end milestone is complete. The next open scope is broader **Record-to-Report**, including additional financial reporting and period-end scenarios, plus the planned Service workstream.
