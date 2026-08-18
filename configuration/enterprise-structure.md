# Enterprise Structure Configuration

## Company Code 9000

| Field | Assigned Value | Status |
|---|---|---|
| Company Code | `9000` | Completed |
| Company Name | TechNova Mfg. GmbH | Completed |
| City | Hamburg | Completed |
| Country / Region | `DE` | Completed |
| Currency | `EUR` | Completed |
| Language Key | `EN` | Completed |
| Chart of Accounts | `BMKG` | Documented |
| Fiscal Year Variant | `K4` | Documented |

## Plant TN01

| Field | Assigned Value | Status |
|---|---|---|
| Plant | `TN01` | Completed |
| Description | TechNova Manufacturing Plant | Completed |
| Company Code Assignment | `9000` | Confirmed |

## Storage Location RM10

| Field | Assigned Value | Status |
|---|---|---|
| Storage Location | `RM10` | Completed & verified |
| Description | Raw materials | Confirmed |
| Plant | `TN01` | Confirmed |

## Purchasing Organization TN01

| Field / Assignment | Assigned Value | Status |
|---|---|---|
| Purchasing Organization | `TN01` | Created |
| Description | TechNova Purchasing | Created |
| Company Code Assignment | `9000` | Completed |
| Plant Assignment | `TN01` | Completed |
| Default / Standard Purchasing Organization | `TN01` → `TN01` | Completed |
| Reference Purchasing Organization | `TN01` | Completed |

## Sales Organization TN01

| Field / Assignment | Assigned Value | Status |
|---|---|---|
| Sales Organization | `TN01` | Created |
| Company Code Assignment | `9000` | Completed |
| Distribution Channel | `10` | Existing entry used / assigned |
| Distribution Channel Description | B2C (Online) | Confirmed |
| Division | `00` | Existing entry used / assigned |
| Division Description | Product Division 00 | Confirmed |
| Sales Area | `TN01 / 10 / 00` | Created / confirmed |

## Documentation Rule

Existing server/demo objects must not be silently reclassified as TechNova-created objects. The project master plan specifically distinguishes confirmed project objects from pre-existing server configuration.

## Evidence

Screenshots belong under:

`evidence/screenshots/enterprise-structure/`
