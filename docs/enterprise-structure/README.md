# Enterprise Structure

## 1. Overview

Enterprise Structure is the organizational foundation of the TechNova Manufacturing GmbH SAP S/4HANA implementation. It defines how the enterprise is represented in SAP and establishes the organizational relationships used by Financial Accounting, Sales and Distribution, Materials Management, Production Planning, Controlling, and related business processes.

A well-defined enterprise structure is essential because transactional processing does not operate independently of organizational assignments. Sales transactions require a sales area, logistics execution depends on plant and shipping-related assignments, inventory is managed at plant and storage-location level, and financial postings are ultimately recorded within a company code.

The implementation therefore treats enterprise structure as a dependency layer that must be established before the downstream business processes are executed.

---

## 2. TechNova Enterprise Scope

The current enterprise design uses the following organizational structure for the primary business scenario:

| Organizational Object | Code | Description / Role |
|---|---:|---|
| Company Code | `9000` | Financial accounting entity for TechNova Mfg. GmbH |
| Sales Organization | `9000` | Commercial organization responsible for sales activities |
| Distribution Channel | `10` | Distribution route used for sales processing |
| Division | `00` | Product/business division used in the sales-area structure |
| Plant | `9000` | Logistics and operational location within the enterprise scope |
| Storage Location | `0001` | Inventory storage subdivision within a plant |
| Chart of Accounts | `BKMG` | Chart of accounts used in the billing-resolution case study |
| Fiscal Year / Period | `2026 / 08` | Financial posting context for the billing-resolution case |
| Customer | `1000000021` | Berlin Office Solutions GmbH; Sold-to / Payer in the case study |

> **Traceability note:** These values represent the documented TechNova enterprise/case-study scope. Practice-system execution values are retained separately when the evidence uses different organizational identifiers.

---

## 3. Understanding the Organizational Objects

### 3.1 Company

A **Company** represents a higher-level legal or corporate grouping in SAP. It can contain one or more company codes and provides a framework for representing entities that belong to the same corporate group.

For this implementation, the business scenario is centered on TechNova Manufacturing GmbH. The detailed financial accounting entity is represented by Company Code `9000`.

### 3.2 Company Code

The **Company Code** is the primary organizational unit for Financial Accounting. It represents the entity for which a complete set of financial statements can be produced.

For TechNova:

- Company Code: `9000`
- Name: `TechNova Mfg. GmbH`
- Country / Region: `DE`
- Currency: `EUR`

The company code becomes the financial anchor for accounting documents, customer and vendor accounting, tax-related postings, and financial reporting.

### 3.3 Plant

The **Plant** represents an operational location where activities such as procurement, inventory management, production, or other logistics processes take place.

Within the project scope, Plant `9000` is the documented TechNova enterprise-scope plant. The implementation also contains practice-system execution evidence using Plant `0001`; that execution value is retained as evidence and is not silently reclassified as Plant `9000`.

### 3.4 Storage Location

A **Storage Location** subdivides inventory within a plant. It allows stock to be managed at a more detailed physical or logical level.

The documented enterprise-scope storage location is `0001`. Storage-location assignments become relevant when material stock, goods movements, picking, goods receipt, and goods issue are executed.

### 3.5 Sales Organization

The **Sales Organization** is the organizational unit responsible for sales activities. It is a key component of the sales-area structure and is used in sales order processing, pricing, billing, reporting, and customer-related sales processes.

The documented TechNova sales organization is `9000` — TechNova Domestic & Export Sales.

### 3.6 Distribution Channel

The **Distribution Channel** describes how products or services are distributed to customers, such as through direct sales, wholesale, retail, or another channel.

The documented distribution channel is `10`.

### 3.7 Division

The **Division** represents a grouping of products or business lines within Sales and Distribution. It participates with the Sales Organization and Distribution Channel in defining the **Sales Area**.

The documented division is `00`.

### 3.8 Sales Area

A **Sales Area** is the combination of:

**Sales Organization + Distribution Channel + Division**

For the TechNova enterprise scope:

```text
Sales Organization  9000
        +
Distribution Channel 10
        +
Division 00
        ↓
Sales Area 9000 / 10 / 00
```

The sales area provides the organizational context for customer sales data, sales documents, pricing, delivery processing, billing, and sales reporting.

### 3.9 Purchasing Organization

A **Purchasing Organization** is responsible for procurement activities and supplier-facing purchasing processes. It can be assigned to company codes and/or plants depending on the organizational design.

The purchasing organization is part of the broader enterprise-structure roadmap. It will be documented with exact executed values when the corresponding procurement configuration is performed and validated.

### 3.10 Purchasing Group

A **Purchasing Group** represents the buyer or group of buyers responsible for procurement activities. It is used primarily for operational purchasing responsibility and reporting.

The purchasing-group configuration remains part of the procurement implementation scope and will be documented after execution.

---

## 4. Key Organizational Relationships

The strength of an SAP enterprise structure comes from the relationships between organizational objects rather than from the individual objects alone.

### Financial Relationship

```text
Company
   ↓
Company Code 9000
   ↓
Financial Accounting
   ↓
G/L / Customer / Vendor / Tax Postings
```

Company Code `9000` provides the accounting context in which financial transactions are recorded.

### Logistics Relationship

```text
Plant
   ↓
Storage Location
   ↓
Material Stock
   ↓
Goods Movements / Inventory Processing
```

The plant provides the operational level, while the storage location provides a more granular stock-management level.

### Sales Relationship

```text
Sales Organization 9000
          +
Distribution Channel 10
          +
Division 00
          ↓
      Sales Area
          ↓
Sales Order → Delivery → Goods Issue → Billing
```

This structure establishes the organizational context for the Order-to-Cash process.

### Cross-Module Relationship

```text
Enterprise Structure
        ↓
   ┌────┼────┬────┬────┐
   ↓    ↓    ↓    ↓    ↓
   FI   MM   SD   PP   CO
   │    │    │    │    │
   └────┴────┴────┴────┴──→ Integrated Business Processes
```

The organizational assignments provide the structural context required for cross-module integration.

---

## 5. Why Enterprise Structure Matters in End-to-End Processing

Enterprise structure directly influences how SAP determines where and how business transactions are processed.

### Example — Order-to-Cash

A customer requirement enters the sales process through a defined sales area. The sales order references the relevant organizational and master-data context. Delivery processing then depends on logistics assignments such as plant and shipping-point determination. Goods issue updates inventory and creates the corresponding material and accounting impacts. Billing subsequently creates the SD billing document and, when account determination and FI prerequisites are satisfied, transfers the financial impact to Financial Accounting.

This means the following chain must remain logically consistent:

```text
Customer
   ↓
Sales Area
   ↓
Sales Order
   ↓
Plant / Logistics
   ↓
Delivery
   ↓
Goods Issue
   ↓
Billing
   ↓
Company Code / FI
   ↓
Accounting Document
```

The current project demonstrates this dependency through the Sales Order `12` milestone and the separate SD-FI billing-resolution case study.

---

## 6. Enterprise Scope vs. Practice-System Execution

The repository deliberately distinguishes between the **TechNova enterprise design** and **values visible in the SAP practice environment**.

For example:

| Object | Enterprise / Case-Study Scope | Practice Execution Evidence |
|---|---|---|
| Company Code | `9000` | `9000` |
| Sales Organization | `9000` | Practice values may differ by scenario |
| Distribution Channel | `10` | Practice values may differ by scenario |
| Division | `00` | Practice values may differ by scenario |
| Plant | `9000` | `0001` in the executed Sales Order scenario |
| Storage Location | `0001` | Recorded according to the executed scenario |
| Customer | `1000000021` | `1000000020` in the executed Sales Order scenario |

This distinction prevents practice-system values from being presented as confirmed enterprise master data without evidence.

---

## 7. Configuration and Governance

Enterprise-structure configuration is treated as controlled foundational configuration. Changes can affect multiple downstream processes and therefore require traceability.

The repository records:

1. Organizational object and purpose
2. Assigned code and description
3. Relevant organizational relationships
4. SAP configuration or transaction area
5. Validation result
6. Transport/change-control information where available
7. Supporting SAP evidence
8. Downstream business-process impact

The documented Company Code configuration is associated with Customizing Request `A4HK901352` and Task `A4HK901353`.

---

## 8. Current Implementation Status

**Status: In Progress**

The Company Code foundation is established and documented. The enterprise-structure model has also been defined at the business-scope level for the current TechNova scenario.

Further organizational objects will be marked as completed only after their configuration and validation are performed in SAP and supported by evidence.

## 9. Evidence Location

Enterprise-structure screenshots are maintained under:

`evidence/screenshots/enterprise-structure/`

The evidence should demonstrate the actual SAP configuration state and should be reviewed before publication for confidential system information.
