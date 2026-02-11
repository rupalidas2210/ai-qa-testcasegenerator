
# Requirement InvApp

## Overview
We are no longer restricting the User from making a negative adjustment on an item that is currently tied to an order (pick shift). The blocker will be removed and negative adjustment will be allowed.

To support this update, the system will now display **IP (in-pick) quantity**. When an order release occurs, any items tied to that release will have an IP quantity shown on the **INV screen**.

---

## Behavior Examples
### Item not tied to pick shift
(Visuals referenced in original document)

### Item tied to an upcoming pick shift
- IP gets updated to reflect quantities that need to be picked.
- QOH is recalculated as: **QOH_new = QOH_original - IP**.

### Remove Adjustment Flow
- User selects **Remove** from the home screen.
- User may adjust quantity using:
  - Minus / Plus buttons
  - Keypad entry
- **Rule:** Maximum removable quantity = updated QOH (after IP is applied)
- If user enters a quantity greater than updated QOH via keypad, system automatically adjusts to max allowable value.
- User confirms adjustment.
- System displays a success snackbar.
- QOH updates accordingly.

---

## Acceptance Criteria
- IP field is displayed at all times.
- When IP = 0, it must display as **0**.
- IP displays quantity allocated for order release.
- IP field directly impacts QOH.
- User cannot remove more than updated QOH.
- If user inputs a value greater than updated QOH, system auto-adjusts to max allowable value.

