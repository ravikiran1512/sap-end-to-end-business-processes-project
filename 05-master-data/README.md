# 05 — Master Data

Master data provides the stable business objects consumed by the TechNova S/4HANA business processes. The repository distinguishes active project master data from practice-system values and historical evidence.

## 1. Active Core Material

**Material `194` — TechNova Business Laptop** is the active core project material.

| Attribute | Current documented value |
|---|---|
| Material | `194` |
| Description | TechNova Business Laptop |
| Material Type | Finished Product |
| Base Unit | `EA` |
| Gross Weight | `2 KG` |
| Net Weight | `1.700 KG` |
| Dimensions | `35 × 24 × 2 cm` |
| Practice Plant | `0001` — AN PLANT – BENGALURU |
| Practice Sales Org | `0001` — Sales Org. 001 |
| Practice Distribution Channel | `01` |
| Classification | Class Type `001` / Class `1000` |
| Tax Classification | `1` — Full tax |
| Availability Check | `02` — Individual requirements |
| Profit Center | `PC0001` |
| Loading Group | `0002` — Forklift |
| Transportation Group | `0004` — Parcel |

Material `194` is reused across MM, SD, PP, inventory, and accounting-related scenarios. The detailed material profile is maintained in the dedicated MM documentation.

## 2. Customer Master

The repository contains customer master data used by separate O2C practice/case-study scenarios. These must remain traceable to their specific execution context rather than being presented as one universal customer record.

- `1000000021` — Berlin Office Solutions GmbH is documented in the enterprise/case-study scope.
- `1000000029` — Delta Electronics is used in the current core O2C execution documentation.
- `1000000020` appears in an earlier Sales Order `12` practice execution.

The customer identifier therefore depends on the specific O2C scenario being documented.

## 3. Procurement Master Data

The completed P2P lifecycle uses the following business objects:

| Business Object | Value |
|---|---|
| Vendor | `12026` — Apex Industrial Supplies GmbH |
| Purchase Order | `4500000149` |
| Procurement Material | TechNova 15.6" Display Panel |
| Quantity | `10 EA` |
| Unit Price | `€50.00` |
| Net Value | `€500.00` |
| Cost Center | `CC9000` |
| Profit Center | `PC9000` |
| Target Expense G/L | `5010032` |
| GR/IR G/L | `2010621` |
| Tax Code | `A1` |

Vendor `12026` became the Accounts Payable business partner for the completed procurement transaction. MIRO created a payable of `€595.00`, which was subsequently cleared through F-53.

## 4. Controlling Master / Assignment Objects

The project also uses controlling objects and account assignments required by the executed manufacturing and period-end close scenarios:

| Object | Value | Usage |
|---|---|---|
| Controlling Area | `9000` | CO integration and settlement |
| Default Cost Center | `CC9000` | Default CO assignment for `5010032` |
| Profit Center | `PC9000` | Procurement / management accounting context |
| Production Order | `1000020` | Manufacturing execution and settlement |
| Material | `194` | Produced finished product |
| Plant | `TN01` | Manufacturing execution context |
| Storage Location | `FG10` | Finished-goods inventory |
| Settled Cost Element / G/L | `5010032` | CO-PC settlement target |

These objects are recorded here as downstream business-process master/assignment references; configuration details remain in `04-configuration/`.

## 5. Master Data Across the End-to-End Model

```text
Material 194
   ├── MM → procurement / inventory
   ├── SD → sales / delivery / billing
   ├── PP → production / goods receipt
   └── FI/CO → accounting and management-accounting integration

Vendor 12026
   ↓
P2P → PO → GR → MIRO → FI → F-53

Customer records
   ↓
O2C → Sales Order → Delivery → PGI → Billing → FI → F-28
```

## 6. Data Governance Rule

The repository follows these rules:

1. **Material `194` is the active core project material.**
2. Practice-system values remain explicitly labelled as practice execution values.
3. Historical identifiers are not silently replaced inside historical evidence.
4. Customer/vendor/material records are tied to their specific business scenario where identifiers differ.
5. Configuration objects such as G/L account determination and OKB9 assignments remain documented in the Configuration section.
6. Evidence supporting master-data execution is centralized under `08-evidence/`.

## 7. Current Implementation Status

**Status: In Progress**

The core material master and the master-data objects required by the completed P2P, O2C, manufacturing, and CO-PC scenarios are documented. Broader master-data coverage remains open for additional enterprise scenarios.

## 8. Evidence

Master-data execution evidence belongs under the centralized structure:

`08-evidence/screenshots/`

Relevant evidence packs are maintained under:

`08-evidence/evidence-packs/`
