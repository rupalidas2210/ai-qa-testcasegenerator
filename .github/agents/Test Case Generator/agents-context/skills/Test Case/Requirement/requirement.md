# Requirement: Unable to Unassign Location & Reserve Label Updates

## Description
**Requirement changes post Demo**

### Updated UI Message
**Unable to Unassign Location**

> This item is currently in a pick shift. You will be able to unassign this location once picking is complete.

---

## Acceptance Criteria

### 1. Unassign Location Message
- The Unassign Location message must match the Figma message exactly.
- Message text:
```
Unable to Unassign Location
This item is currently in a pick shift. You will be able to unassign this location once picking is complete.
```

### 2. Reserve Labels
- Reserve labels must not include any item information.
  - Labels should display only:
    - Item
    - Barcode

- Barcode requirements:
  - Barcode must be scannable.
  - Barcode must match the location code on the label, but without the "-" character.

---
