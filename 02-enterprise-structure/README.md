# 02 — Enterprise Structure

The organizational foundation of the TechNova Manufacturing GmbH SAP S/4HANA implementation.

## Current Scope

| Organizational Object | Code | Current Status | Role |
|---|---:|---|---|
| Company Code | `9000` | **Established** | Financial accounting entity for TechNova Mfg. GmbH |
| Sales Organization | `9000` | **Defined** | Sales execution context |
| Distribution Channel | `10` | **Defined** | Distribution route used for sales processing |
| Division | `00` | **Defined** | Product/business division |
| Sales Area | `9000 / 10 / 00` | **Defined** | Sales organizational combination |
| Plant | `9000` | **Defined** | Documented TechNova logistics/operational scope |
| Storage Location | `0001` | **Defined** | Inventory subdivision |
| Chart of Accounts | `BKMG` | **Established / Used** | Financial accounting framework used in the project |
| Fiscal Year | `2026` | **Used** | Current project financial context |
| Fiscal Period | `09` | **Used in current close** | Manufacturing CO-PC period-end settlement |

## Company Code Foundation

Company Code `9000` — **TechNova Mfg. GmbH** is the established FI anchor for the project. The documented configuration uses country/region `DE` and currency `EUR`.

The Company Code configuration is associated with Customizing Request `A4HK901352` and Task `A4HK901353`.

## Sales Organization Structure

The documented sales structure is:

```text
Sales Organization 9000
        +
Distribution Channel 10
        +
Division 00
        ↓
Sales Area 9000 / 10 / 00
```

This provides the organizational context for sales order processing, delivery, billing, and sales reporting.

## Logistics Structure

```text
Plant 9000
   ↓
Storage Location 0001
   ↓
Inventory Management
   ↓
Goods Movements / Logistics Execution
```

The repository also preserves practice-system execution values where the SAP exercise environment uses different organizational identifiers. These are not silently reclassified as TechNova enterprise master data.

## Cross-Module Dependency

The enterprise structure provides the organizational context for the project's integrated workstreams:

```text
Enterprise Structure
        ↓
   ┌────┼────┬────┬────┐
   ↓    ↓    ↓    ↓    ↓
   FI   MM   SD   PP   CO
   │    │    │    │    │
   └────┴────┴────┴────┴──→ End-to-End Processes
```

Examples already executed in the project include O2C, P2P, manufacturing execution, and manufacturing CO-PC period-end settlement.

## Procurement Structure

Purchasing Organization and Purchasing Group remain part of the broader procurement design. Exact values should only be marked as established after corresponding SAP configuration and validation evidence is available.

## Enterprise Structure vs. Practice-System Values

The project deliberately distinguishes the **TechNova enterprise design** from values visible in the SAP practice environment. For example, the documented enterprise plant is `9000`, while some executed practice scenarios use Plant `0001`. The same principle applies to other practice-system organizational and master-data values.

This separation preserves traceability and prevents exercise-environment values from being presented as confirmed enterprise configuration.

## Current Implementation Status

**Status: In Progress**

The enterprise model and Company Code foundation are established, and the core organizational relationships used by the project are documented. Remaining organizational objects will be promoted to **Established** only after SAP configuration and validation evidence is available.

## Evidence

Enterprise-structure evidence belongs under the centralized evidence structure:

`08-evidence/screenshots/enterprise-structure/`

`08-evidence/` is the single source of truth for execution screenshots and evidence packs.
