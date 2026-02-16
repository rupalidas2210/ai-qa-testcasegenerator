
# InvApplocationValidation

## Behavior Update
Update the UI to change the title on the adjustment screen based on the value of the `locationValidationRequired` flag.

### If `locationValidationRequired` is **true**
- Show: **Scan location** (title/label)
- User must scan location, then proceed to adjustment screen (**Input adjustment and move items**)

### If `locationValidationRequired` is **false**
- Show: **Input adjustment and move items** (title/label)
- Directly show adjustment screen, skipping location scan

## Current Behavior (Before)
The screen displays the label: **Scan location**

## Expected Behavior (After)
The screen displays: **Input adjustment and move items** when the flag is false.

## Acceptance Criteria
- The adjustment screen title changes correctly according to the flag.
- The user experience matches the described flow for each flag value.
- Ensure consistent wording:
  - "Scan location" when true
  - "Input adjustment and move items" when false
