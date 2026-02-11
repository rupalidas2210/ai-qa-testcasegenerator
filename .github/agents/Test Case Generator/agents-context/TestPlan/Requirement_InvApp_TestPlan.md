# InvApp - Test Plan

## 1. Purpose and Quality Objectives

### Testing Goals
- Validate the removal of restrictions on negative adjustments for items tied to order pick shifts
- Verify accurate display and calculation of IP (in-pick) quantity across all scenarios
- Ensure QOH (Quantity on Hand) recalculation is accurate when IP is applied
- Validate user interface controls and input validation for the Remove Adjustment flow
- Confirm system behavior meets all acceptance criteria

### Success Criteria
- 100% requirements traceability achieved
- All test scenarios executed with expected results
- Zero critical/high severity defects in production
- Complete coverage of functional, negative, edge, and integration scenarios

### Definition of Complete Test Coverage
- All business rules validated
- All acceptance criteria met
- All user interaction paths tested (button controls, keypad entry)
- All data validation scenarios covered (boundary values, invalid inputs)
- All state transitions verified (IP=0, IP>0, QOH updates)
- Error handling and user feedback validated

---

## 2. Scope

### In-Scope
- IP (in-pick) quantity display on INV screen
- QOH recalculation logic when orders are released (QOH_new = QOH_original - IP)
- Remove Adjustment workflow via home screen
- Quantity adjustment controls (Minus/Plus buttons, Keypad entry)
- Maximum removable quantity validation (≤ updated QOH)
- Auto-adjustment of keypad entries exceeding max allowable value
- Success snackbar display after adjustment confirmation
- QOH update after successful adjustment
- IP display behavior when IP = 0

### Out-of-Scope
- Order release functionality (assumed to be working)
- Pick shift creation and management
- Other adjustment types (Add, Transfer)
- Inventory screens other than INV screen
- Backend inventory management systems
- Historical reporting of adjustments

### Assumptions
- Order release system is functioning correctly and updates IP values
- INV screen is accessible to authorized users
- User has necessary permissions to perform Remove adjustments
- System has network connectivity for real-time updates

### Constraints
- Testing limited to Remove Adjustment flow only
- IP calculation depends on external order release process

### Dependencies
- Order management system must be available for creating test scenarios with active pick shifts
- INV screen must be deployed with IP field integration
- Backend API for QOH calculation must be accessible

---

## 3. Requirements Traceability Matrix (RTM)

| Req ID  | Requirement Description                                      | Acceptance Criteria                                         | Test Scenario IDs                          | Test Case IDs |
|---------|-------------------------------------------------------------|-------------------------------------------------------------|--------------------------------------------|---------------|
| REQ-001 | Display IP quantity on INV screen at all times              | IP field visible; displays 0 when no pick shift            | TS-001, TS-002                             | TBD           |
| REQ-002 | Update IP when order release occurs                         | IP reflects quantities allocated for pick shift            | TS-003, TS-004                             | TBD           |
| REQ-003 | Recalculate QOH when IP is updated                          | QOH_new = QOH_original - IP                                | TS-005, TS-006, TS-007                     | TBD           |
| REQ-004 | Allow negative adjustment on items tied to pick shift       | Negative adjustment permitted (blocker removed)            | TS-008, TS-009                             | TBD           |
| REQ-005 | Remove Adjustment accessible from home screen               | User can navigate to Remove Adjustment                     | TS-010, TS-011                             | TBD           |
| REQ-006 | Quantity adjustment via Minus/Plus buttons                  | User can adjust quantity using buttons                     | TS-012, TS-013, TS-014                     | TBD           |
| REQ-007 | Quantity adjustment via keypad entry                        | User can enter quantity manually                           | TS-015, TS-016                             | TBD           |
| REQ-008 | Maximum removable quantity = updated QOH                    | System enforces max limit based on QOH after IP applied    | TS-017, TS-018, TS-019                     | TBD           |
| REQ-009 | Auto-adjust keypad entry exceeding updated QOH              | System automatically caps to max allowable value           | TS-020, TS-021, TS-022                     | TBD           |
| REQ-010 | Confirm adjustment and display success snackbar             | User confirms; success message displayed                   | TS-023, TS-024                             | TBD           |
| REQ-011 | Update QOH after adjustment confirmation                    | QOH reflects new quantity post-adjustment                  | TS-025, TS-026, TS-027                     | TBD           |
| REQ-012 | IP displays 0 when no pick shift                            | IP = 0 shown explicitly                                    | TS-028, TS-029                             | TBD           |

---

## 4. System Overview and Test Boundaries

### High-Level Architecture
```
[User Interface - INV Screen]
          ↓
[Frontend Application Layer]
          ↓
[API Gateway / Backend Services]
          ↓
[Inventory Management Service]
          ↓
[Database - Inventory Tables]
          ↓
[Order Management System - Pick Shift Data]
```

### Data Flow
1. Order release triggers IP calculation
2. IP value pushed to Inventory Management Service
3. INV screen fetches IP and QOH values
4. QOH recalculated as QOH_original - IP
5. User initiates Remove Adjustment
6. Frontend validates input against updated QOH
7. Backend processes adjustment
8. Database updates QOH
9. Success feedback to user

### Test Boundaries
- **UI Testing**: INV screen display, controls, validation messages
- **Functional Testing**: QOH/IP calculations, adjustment workflow
- **Integration Testing**: Order system → Inventory system data sync
- **Data Validation**: Input constraints, boundary conditions

### Real vs Mocked Components
- **Real**: INV screen UI, Remove Adjustment workflow, database operations
- **Mocked (if needed)**: Order release system (for controlled IP scenarios)

---

## 5. Feature and Business Rule Breakdown

### Feature 1: IP (In-Pick) Quantity Display
**Sub-Features:**
- IP field always visible on INV screen
- IP displays allocated quantity for order release
- IP shows 0 when no pick shift active

**Business Rules:**
- BR-001: IP field must be present at all times
- BR-002: When IP = 0, display must show "0" explicitly (not blank/null)
- BR-003: IP value sourced from order release system
- BR-004: IP updates in real-time when order release occurs

**Field-Level Validations:**
- IP is read-only (display-only field)
- IP must be non-negative integer
- IP format: numeric display

**State Transitions:**
- State 1: Item not tied to pick shift → IP = 0
- State 2: Item tied to upcoming pick shift → IP = allocated quantity
- State 3: Pick shift completed → IP resets to 0

---

### Feature 2: QOH Recalculation
**Sub-Features:**
- Automatic QOH calculation when IP is updated
- Display of updated QOH on INV screen

**Business Rules:**
- BR-005: QOH_new = QOH_original - IP
- BR-006: QOH recalculation happens immediately when IP changes
- BR-007: QOH_new cannot be negative

**Field-Level Validations:**
- QOH must be numeric
- QOH precision: integer values
- QOH_new must reflect formula accurately

**State Transitions:**
- QOH_original → IP assignment → QOH_new calculated → Display updated

---

### Feature 3: Remove Adjustment Workflow
**Sub-Features:**
- Navigate to Remove Adjustment from home screen
- Adjust quantity using Minus/Plus buttons
- Adjust quantity using keypad
- Confirm adjustment
- Success notification
- QOH update post-adjustment

**Business Rules:**
- BR-008: Negative adjustment allowed on items tied to pick shift (blocker removed)
- BR-009: Maximum removable quantity = updated QOH (QOH_original - IP)
- BR-010: System auto-adjusts keypad entry if exceeds max allowable value
- BR-011: User must confirm adjustment before QOH changes
- BR-012: Success snackbar displayed after confirmation
- BR-013: QOH updated only after successful confirmation

**Field-Level Validations:**
- Quantity input: numeric only
- Quantity range: 0 to updated QOH
- Buttons: Minus decreases, Plus increases
- Keypad: accepts numeric characters, decimal handling (if applicable)

**Workflow Rules:**
- Step 1: User selects Remove from home screen
- Step 2: System displays current item with QOH and IP
- Step 3: User adjusts quantity
- Step 4: System validates input ≤ updated QOH
- Step 5: User confirms
- Step 6: System processes adjustment
- Step 7: Success snackbar shown
- Step 8: QOH updated and displayed

---

## 6. Coverage Model

### 6.1 Functional Coverage
**Happy Path:**
- Display IP when no pick shift (IP = 0)
- Display IP when pick shift active (IP > 0)
- Calculate QOH correctly (QOH_new = QOH_original - IP)
- Remove adjustment using Minus button
- Remove adjustment using Plus button
- Remove adjustment using keypad within limit
- Confirm adjustment and see success message
- Verify QOH updated after adjustment

**Alternate Paths:**
- Adjust quantity to exactly updated QOH
- Adjust quantity to zero
- Cancel adjustment workflow

**Negative Cases:**
- Attempt to enter quantity exceeding updated QOH via keypad
- Attempt to increase quantity beyond updated QOH using Plus button
- Invalid input formats (letters, special characters)
- Enter negative quantity directly

---

### 6.2 Data Coverage
**Boundaries:**
- IP = 0 (minimum)
- IP = QOH_original (maximum realistic scenario)
- Adjustment quantity = 0 (minimum)
- Adjustment quantity = updated QOH (maximum allowed)
- Adjustment quantity = updated QOH + 1 (exceeds limit)

**Equivalence Classes:**
- Valid IP values: 0, 1-999, 1000+
- Valid adjustment quantities: 0, within limit, at limit
- Invalid keypad entries: negative numbers, letters, special chars, exceeds limit

**Null/Empty:**
- IP cannot be null (must display 0)
- Adjustment quantity cannot be blank

**Invalid Formats:**
- Alphabetic characters in keypad
- Special characters in keypad
- Decimal values (if system expects integers)

---

### 6.3 State/Workflow Coverage
**State Transitions:**
1. Item with no pick shift (IP=0) → Order release → Item with pick shift (IP>0)
2. QOH_original → IP assigned → QOH_new calculated
3. INV screen → Navigate to Remove Adjustment → Adjust → Confirm → View updated QOH

**Workflow Variations:**
- Normal flow: Home → Remove → Adjust → Confirm → Success
- Cancel flow: Home → Remove → Adjust → Cancel → Return to Home
- Error flow: Home → Remove → Adjust (exceeds limit) → Auto-correct → Confirm → Success

---

### 6.4 Role and Permission Coverage
- Authorized user with Remove Adjustment permission
- Unauthorized user attempting Remove Adjustment (if permission structure exists)

---

### 6.5 Platform/API Version Coverage
- INV screen on different device types (mobile, tablet, desktop if applicable)
- API version compatibility for QOH/IP calculations

---

### 6.6 Integration Coverage
**Integration Points:**
- Order Management System → Inventory System (IP data sync)
- Remove Adjustment UI → Backend API (adjustment processing)
- Backend API → Database (QOH update)

**Success Scenarios:**
- Successful IP update from order release
- Successful adjustment submission
- Successful QOH update in database

**Failure Scenarios:**
- IP data sync failure (order system unavailable)
- Backend API timeout during adjustment
- Database update failure

---

### 6.7 Non-Functional Coverage
**Performance:**
- IP display loads within acceptable time
- QOH recalculation happens in real-time
- Adjustment confirmation processes quickly

**Security:**
- Only authorized users can access Remove Adjustment
- Input validation prevents injection attacks

**Usability:**
- Clear error messages when input exceeds limit
- Success snackbar is visible and understandable
- Controls are intuitive (Minus/Plus buttons)

---

## 7. Test Scenario Catalog

### 7.1 IP Display Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations              | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|------------------------------------|---------------------------------------------------|---------|
| TS-001      | Verify IP displays 0 when no pick shift          | Item not tied to any order             | IP = 0                             | INV screen shows IP = 0                           | REQ-001 |
| TS-002      | Verify IP field is always visible                | Item on INV screen                     | Various items with/without pick shift | IP field present on screen                        | REQ-001 |
| TS-003      | Verify IP updates when order released            | Item with QOH, order release triggered | IP = allocated quantity            | INV screen shows updated IP value                 | REQ-002 |
| TS-004      | Verify IP reflects correct pick quantity         | Order release with 10 items            | IP = 10                            | INV screen displays IP = 10                       | REQ-002 |

---

### 7.2 QOH Recalculation Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-005      | Verify QOH recalculation formula                 | QOH_original = 100, IP = 10            | IP assigned                         | QOH_new = 90 (100 - 10)                           | REQ-003 |
| TS-006      | Verify QOH updates in real-time                  | Order release occurs                   | IP changes from 0 to 20             | QOH recalculated immediately                      | REQ-003 |
| TS-007      | Verify QOH when IP equals QOH_original           | QOH_original = 50, IP = 50             | Full allocation                     | QOH_new = 0                                       | REQ-003 |

---

### 7.3 Negative Adjustment Allowed Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-008      | Verify negative adjustment on item with pick shift | Item tied to pick shift (IP > 0)     | User attempts Remove Adjustment     | Adjustment allowed (no blocker)                   | REQ-004 |
| TS-009      | Verify blocker is removed                        | Previously blocker existed             | Remove Adjustment flow              | User can proceed without restrictions             | REQ-004 |

---

### 7.4 Navigation Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-010      | Verify Remove option on home screen              | User on home screen                    | View home screen options            | Remove option visible and clickable               | REQ-005 |
| TS-011      | Verify navigation to Remove Adjustment           | User selects Remove from home          | Click Remove option                 | Remove Adjustment screen opens                    | REQ-005 |

---

### 7.5 Button Control Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-012      | Verify Minus button decreases quantity           | Remove Adjustment screen, quantity = 5 | Click Minus button                  | Quantity decreases by 1 (becomes 4)               | REQ-006 |
| TS-013      | Verify Plus button increases quantity            | Remove Adjustment screen, quantity = 5 | Click Plus button                   | Quantity increases by 1 (becomes 6)               | REQ-006 |
| TS-014      | Verify Minus button at minimum boundary          | Quantity = 0                           | Click Minus button                  | Quantity remains 0 (cannot go negative)           | REQ-006 |

---

### 7.6 Keypad Entry Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-015      | Verify keypad entry within limit                 | Updated QOH = 50                       | User enters 30 via keypad           | System accepts 30 as adjustment quantity          | REQ-007 |
| TS-016      | Verify keypad entry of 0                         | Updated QOH = 50                       | User enters 0 via keypad            | System accepts 0 as adjustment quantity           | REQ-007 |

---

### 7.7 Maximum Removable Quantity Validation Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-017      | Verify max removable quantity = updated QOH      | QOH_original = 100, IP = 20, QOH_new = 80 | User attempts to remove 80       | System allows removal of 80 (max limit)           | REQ-008 |
| TS-018      | Verify buttons cannot exceed updated QOH         | Updated QOH = 80, quantity = 80        | Click Plus button                   | Quantity remains 80 (cannot exceed limit)         | REQ-008 |
| TS-019      | Verify validation message when exceeding limit   | Updated QOH = 80                       | Attempt to adjust beyond 80         | System prevents or auto-adjusts                   | REQ-008 |

---

### 7.8 Auto-Adjust Keypad Entry Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-020      | Verify auto-adjust when keypad exceeds limit     | Updated QOH = 50                       | User enters 70 via keypad           | System auto-adjusts to 50                         | REQ-009 |
| TS-021      | Verify auto-adjust at exact limit                | Updated QOH = 50                       | User enters 50 via keypad           | System accepts 50 (no auto-adjust needed)         | REQ-009 |
| TS-022      | Verify auto-adjust with large excess value       | Updated QOH = 50                       | User enters 9999 via keypad         | System auto-adjusts to 50                         | REQ-009 |

---

### 7.9 Confirmation and Success Message Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-023      | Verify confirmation button functionality         | Adjustment quantity set                | User clicks Confirm                 | System processes adjustment                       | REQ-010 |
| TS-024      | Verify success snackbar display                  | Adjustment confirmed                   | System completes adjustment         | Success snackbar appears with message             | REQ-010 |

---

### 7.10 QOH Update Post-Adjustment Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-025      | Verify QOH updates after adjustment              | QOH_new = 80, remove 10                | Adjustment confirmed                | QOH = 70 displayed                                | REQ-011 |
| TS-026      | Verify QOH update persists after screen refresh  | Adjustment completed                   | User refreshes INV screen           | Updated QOH persists                              | REQ-011 |
| TS-027      | Verify QOH does not update on cancel             | Adjustment set but cancelled           | User cancels before confirm         | QOH remains unchanged                             | REQ-011 |

---

### 7.11 IP Zero Display Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-028      | Verify IP displays "0" explicitly when no pick shift | Item not in pick shift              | IP = 0                              | INV screen shows "0" (not blank)                  | REQ-012 |
| TS-029      | Verify IP resets to 0 after pick shift completion | Pick shift completed                 | IP returns to 0                     | INV screen displays IP = 0                        | REQ-012 |

---

### 7.12 Negative Test Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-030      | Verify invalid keypad input (alphabetic)         | Remove Adjustment screen               | User enters "ABC" via keypad        | System rejects or ignores input                   | REQ-007 |
| TS-031      | Verify invalid keypad input (special characters) | Remove Adjustment screen               | User enters "@#$" via keypad        | System rejects or ignores input                   | REQ-007 |
| TS-032      | Verify negative number entry via keypad          | Remove Adjustment screen               | User enters "-10" via keypad        | System rejects or adjusts to 0                    | REQ-007 |
| TS-033      | Verify decimal entry if system expects integer   | Remove Adjustment screen               | User enters "5.5" via keypad        | System handles gracefully (round or reject)       | REQ-007 |

---

### 7.13 Edge Test Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-034      | Verify behavior when QOH_original = 0            | QOH = 0, no pick shift                 | IP = 0, QOH_new = 0                 | Remove Adjustment not possible or quantity = 0    | REQ-003 |
| TS-035      | Verify behavior with very large IP value         | QOH_original = 10000, IP = 9999        | QOH_new = 1                         | System calculates correctly, max removable = 1    | REQ-003 |
| TS-036      | Verify rapid button clicks (Plus/Minus)          | Remove Adjustment screen               | User clicks Plus 10 times rapidly   | Quantity updates correctly, respects limit        | REQ-006 |
| TS-037      | Verify adjustment at exact updated QOH           | Updated QOH = 50                       | Remove exactly 50                   | QOH becomes 0 after adjustment                    | REQ-008 |
| TS-038      | Verify concurrent adjustments (if multi-user)    | Two users adjusting same item          | Concurrent Remove operations        | System handles concurrency (lock/optimistic)      | REQ-011 |

---

### 7.14 Integration Test Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-039      | Verify IP sync from order system to inventory    | Order release triggered                | Order system sends IP data          | Inventory system receives and displays IP         | REQ-002 |
| TS-040      | Verify adjustment API call to backend            | User confirms adjustment               | Frontend sends adjustment request   | Backend processes and responds with success       | REQ-010 |
| TS-041      | Verify database update after adjustment          | Adjustment confirmed                   | Backend updates database            | Database reflects new QOH value                   | REQ-011 |
| TS-042      | Verify error handling when order system down     | Order system unavailable               | IP data not received                | System displays last known IP or error message    | REQ-002 |

---

### 7.15 End-to-End Test Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-043      | E2E: Order release to adjustment with IP > 0     | Item with QOH = 100                    | Order released (IP = 30), remove 20 | IP = 30, QOH_new = 70, adjust to 50, success      | Multiple |
| TS-044      | E2E: Adjustment on item with no pick shift       | Item with QOH = 100, IP = 0            | Remove 20 via keypad                | IP = 0, QOH = 100, adjust to 80, success          | Multiple |
| TS-045      | E2E: Adjustment exceeding limit, auto-correct    | QOH = 50, IP = 10, QOH_new = 40        | Enter 50 via keypad                 | System auto-corrects to 40, adjust, success       | Multiple |

---

### 7.16 Regression Test Scenarios

| Scenario ID | Description                                      | Preconditions                          | Input/Data Variations               | Expected Result                                   | Req ID  |
|-------------|--------------------------------------------------|----------------------------------------|-------------------------------------|---------------------------------------------------|---------|
| TS-046      | Verify previous blocker is not reintroduced      | Item tied to pick shift                | Negative adjustment attempted       | No blocker appears, adjustment proceeds           | REQ-004 |
| TS-047      | Verify existing QOH display functionality        | INV screen loaded                      | View QOH value                      | QOH displayed correctly                           | REQ-003 |
| TS-048      | Verify other adjustment types unaffected         | Add Adjustment flow                    | User performs Add operation         | Add Adjustment works normally (if in scope)       | N/A     |

---

## 8. Test Data Strategy

### Required Data Sets

#### Valid Data
- **Items with no pick shift:**
  - Item ID: ITEM-001, QOH = 100, IP = 0
  - Item ID: ITEM-002, QOH = 50, IP = 0
  
- **Items with active pick shift:**
  - Item ID: ITEM-003, QOH_original = 100, IP = 20, QOH_new = 80
  - Item ID: ITEM-004, QOH_original = 200, IP = 50, QOH_new = 150
  
- **Edge case items:**
  - Item ID: ITEM-005, QOH_original = 10, IP = 10, QOH_new = 0
  - Item ID: ITEM-006, QOH_original = 0, IP = 0, QOH_new = 0
  - Item ID: ITEM-007, QOH_original = 10000, IP = 9999, QOH_new = 1

#### Invalid Data
- Alphabetic characters: "ABC", "xyz"
- Special characters: "@#$", "***"
- Negative numbers: "-10", "-5"
- Decimal values: "5.5", "10.75" (if system expects integers)
- Exceeds limit values: 100 (when updated QOH = 50)

#### Test User Roles
- **Standard User:** Has permission to perform Remove Adjustments
- **Admin User:** Full inventory management permissions
- **Unauthorized User:** No Remove Adjustment permission (if applicable)

### Data Setup Approach
- **Pre-populate inventory database** with test items
- **Trigger order releases** to set IP values for test scenarios
- **Automate data setup scripts** for repeatable test environments

### Data Cleanup
- **Reset QOH and IP values** after each test case
- **Remove test items** from database at end of test suite
- **Archive test data** for regression testing

---

## 9. Test Environment and Configuration

### Test Environments
- **DEV Environment:** For initial development testing
- **QA Environment:** For comprehensive functional and integration testing
- **Staging Environment:** For pre-production validation and E2E testing
- **Production-like Environment:** For performance and regression testing

### Configuration Requirements
- **INV Screen:** Deployed with IP field integration
- **Order Management System:** Accessible for triggering order releases
- **Backend API:** Inventory adjustment endpoints available
- **Database:** Test inventory data populated

### Feature Flags
- Feature flag for IP display toggle (if applicable)
- Feature flag for negative adjustment blocker removal

### Stubs and Mocks
- **Mock Order Release System:** For controlled IP value injection
- **Stub Backend API:** For testing frontend validation in isolation

### Versioning Assumptions
- Frontend version: Latest with IP integration
- Backend API version: Compatible with new QOH calculation logic
- Database schema version: Includes IP column

---

## 10. Entry and Exit Criteria

### Entry Criteria
- INV screen deployed with IP field visible
- IP calculation logic integrated with order release system
- QOH recalculation formula implemented (QOH_new = QOH_original - IP)
- Remove Adjustment workflow accessible from home screen
- Test environment configured with test data
- Test cases reviewed and approved by stakeholders

### Exit Criteria
- **100% RTM Coverage:** All requirements mapped to executed test cases
- **All Test Scenarios Executed:** 45 test scenarios completed with results documented
- **Critical/High Defects Resolved:** Zero P0/P1 defects open
- **Medium/Low Defects Triaged:** P2/P3 defects documented for future sprints
- **Acceptance Criteria Met:** All 7 acceptance criteria validated
- **Regression Testing Complete:** Core flows tested post-changes
- **Performance Benchmarks Met:** IP display and QOH update within acceptable time
- **Sign-off Obtained:** Product Owner and QA Lead approval

---

## 11. Defect Management

### Severity Definitions
- **Critical (P0):** System crash, data corruption, blocker reinstated, QOH calculation incorrect
- **High (P1):** Major functionality broken (IP not updating, auto-adjust not working)
- **Medium (P2):** Minor functionality issues (UI glitches, validation message unclear)
- **Low (P3):** Cosmetic issues (typos, alignment)

### Priority Definitions
- **P0:** Must fix before release
- **P1:** Fix in current sprint
- **P2:** Schedule for next sprint
- **P3:** Backlog for future consideration

### Retest Rules
- All P0/P1 defects must be retested after fix
- Regression testing required for fixes impacting core QOH logic

### Stop-Ship Criteria
- Any P0 defect open
- QOH calculation formula incorrect
- Negative adjustment blocker reintroduced
- IP not displaying on INV screen

---

## 12. Test Levels and Types

### Test Levels
- **Unit Testing:** Backend QOH calculation logic (Dev responsibility)
- **Component Testing:** IP display component, button controls
- **Integration Testing:** Order system → Inventory system sync
- **System Testing:** End-to-end Remove Adjustment workflow
- **Acceptance Testing:** Validate against acceptance criteria

### Test Types
- **Functional Testing:** Core features (IP display, QOH recalculation, adjustment workflow)
- **Smoke Testing:** Critical paths (navigate to Remove, adjust, confirm)
- **API Testing:** Backend endpoints for adjustment processing
- **UI Testing:** INV screen display, controls, validation messages
- **Integration Testing:** Order release to IP update
- **End-to-End Testing:** Order release → IP update → Remove Adjustment → QOH update
- **Regression Testing:** Verify existing flows not impacted
- **Negative Testing:** Invalid inputs, exceeding limits
- **Edge Testing:** Boundary values, concurrent operations

### Manual vs Automated
- **Manual Testing:** Exploratory testing, usability validation, initial smoke tests
- **Automated Testing:** Regression suite, API tests, QOH calculation validation

---

## 13. Risk-Based Testing

### High-Risk Areas
1. **QOH Calculation Accuracy:** Formula error leads to incorrect inventory counts
2. **Negative Adjustment Blocker Removal:** Regression risk if blocker reappears
3. **Auto-Adjust Logic:** Incorrect capping leads to data inconsistency
4. **IP Data Sync:** Order system failure causes stale IP values

### Mandatory Tests Per Risk
- **QOH Calculation:**
  - TS-005 (formula validation)
  - TS-006 (real-time update)
  - TS-007 (edge case: IP = QOH_original)
  
- **Blocker Removal:**
  - TS-008 (negative adjustment allowed)
  - TS-046 (regression: blocker not reintroduced)
  
- **Auto-Adjust Logic:**
  - TS-020 (auto-adjust exceeding limit)
  - TS-022 (large excess value)
  
- **IP Data Sync:**
  - TS-039 (integration: IP sync)
  - TS-042 (error handling: order system down)

---

## 14. Test Execution Summary

### Test Metrics to Track
- Total test scenarios: 48
- Test scenarios executed: TBD
- Test scenarios passed: TBD
- Test scenarios failed: TBD
- Defects found: TBD
- Defects resolved: TBD
- Requirements coverage: 100% (12/12 requirements)

### Test Execution Schedule
- **Week 1:** Functional testing (IP display, QOH calculation)
- **Week 2:** Adjustment workflow testing (buttons, keypad, validation)
- **Week 3:** Integration and E2E testing
- **Week 4:** Regression, negative, and edge testing
- **Week 5:** UAT and final sign-off

---

## 15. Sign-off

| Role               | Name | Date | Signature |
|--------------------|------|------|-----------|
| QA Lead            |      |      |           |
| Product Owner      |      |      |           |
| Development Lead   |      |      |           |

---

## 16. Appendix

### Glossary
- **IP (In-Pick):** Quantity allocated for order pick shift
- **QOH (Quantity on Hand):** Current available inventory quantity
- **Remove Adjustment:** Inventory adjustment operation to reduce quantity
- **Pick Shift:** Order fulfillment operation requiring items from inventory

### References
- Requirement Document: "Requirement InvApp"
- API Documentation: [Link to API docs]
- Design Mockups: [Link to UI designs]

---

## Test Plan Approval

This Test Plan has been created to ensure comprehensive coverage of the InvApp requirement. All test scenarios are traceable to requirements through the RTM. Test cases will be generated separately using the "Generate Zephyr Test Case" skill.

**Test Plan Version:** 1.0  
**Date Created:** February 10, 2026  
**Created By:** QA Test Architect  
**Status:** Ready for Test Case Generation
