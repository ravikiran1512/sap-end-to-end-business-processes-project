# 09 — Lessons Learned

## Implementation Lessons

- Enterprise structure must be established as a dependency layer for downstream processes.
- In S/4HANA, CO and FI are integrated through the Universal Journal; CO Version-to-Ledger alignment is therefore a critical posting prerequisite.
- A billing document can exist successfully while FI transfer remains blocked by account determination or accounting prerequisites.
- MIGO Goods Receipt establishes the GR/IR position required for subsequent invoice verification in MIRO.
- Practice-system identifiers must remain traceable and should not be silently rewritten to match a conceptual enterprise design.

## Documentation Standard

Every milestone should record the business purpose, SAP transaction/configuration, exact executed values, validation result, evidence, and next dependency.
