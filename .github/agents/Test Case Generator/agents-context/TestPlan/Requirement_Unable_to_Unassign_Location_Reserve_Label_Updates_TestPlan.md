# Test Plan: Unable to Unassign Location & Reserve Label Updates

## 1. Purpose and Quality Objectives

### Testing Goals
- Validate the updated UI message for "Unable to Unassign Location" matches Figma specifications exactly
- Ensure Reserve labels display only required information (Item and Barcode)
- Verify barcode scannability and correct format (location code without "-" character)
- Ensure system behavior during active pick shifts prevents location unassignment

### Success Criteria
- 100% Requirements Traceability Matrix coverage
- All acceptance criteria validated through test execution
- Zero critical defects in UI messaging and label generation
- Barcode scanning success rate of 100%

### Definition of Complete Test Coverage
Complete coverage is achieved when:
- All functional requirements are tested (positive, negative, edge cases)
- All UI messages are validated against Figma specifications
- All barcode formats and scannability scenarios are verified
- All user workflows involving location unassignment and label generation are tested
- Integration points with pick shift management are validated

---

## 2. Scope

### In-Scope
- UI message validation for "Unable to Unassign Location"
- Reserve label format and content validation
- Barcode generation and scannability testing
- Location unassignment functionality during active pick shifts
- Integration with pick shift management system

### Out-of-Scope
- Pick shift creation and management workflows (assumed functional)
- Overall warehouse management system functionality
- Label printer hardware configuration
- Physical label printing quality (beyond barcode scannability)

### Assumptions
- Pick shift management system is functional and provides accurate status
- Figma design specifications are final and approved
- Test environment has access to barcode scanning capability
- Location codes follow established format standards

### Constraints
- Testing limited to scenarios where items are in active pick shifts
- Barcode testing requires physical or virtual scanner capability

### Dependencies
- Access to Figma design specifications for message validation
- Functional pick shift management system in test environment
- Barcode scanner device or scanning software
- Test data with valid location codes and items

---

## 3. Requirements Traceability Matrix (RTM)

| Req ID | Requirement Description | Acceptance Criteria | Test Scenario IDs | Priority | Status |
|--------|------------------------|---------------------|-------------------|----------|--------|
| REQ-01 | Unassign Location Message Display | AC1: Message must match Figma exactly | TS-001, TS-002, TS-003 | High | Active |
| REQ-02 | Reserve Label Content | AC2: Labels display only Item and Barcode | TS-004, TS-005, TS-006 | High | Active |
| REQ-03 | Barcode Scannability | AC3: Barcode must be scannable | TS-007, TS-008, TS-009 | Critical | Active |
| REQ-04 | Barcode Format | AC4: Barcode matches location code without "-" | TS-010, TS-011, TS-012 | High | Active |
| REQ-05 | Location Unassignment Prevention | Item in active pick shift cannot unassign location | TS-001, TS-013, TS-014 | High | Active |

**Coverage Summary:**
- Total Requirements: 5
- Total Test Scenarios: 14
- Coverage: 100%

---

## 4. System Overview and Test Boundaries

### High-Level Architecture
```
[UI Layer] ← → [Business Logic Layer] ← → [Pick Shift Service]
                       ↓
              [Label Generation Service]
                       ↓
              [Barcode Generator]
                       ↓
                  [Database]
```

### Components Involved
1. **UI Layer**: Location management interface, message display
2. **Business Logic**: Location unassignment logic, pick shift validation
3. **Pick Shift Service**: Active pick shift status provider
4. **Label Generation Service**: Reserve label creation
5. **Barcode Generator**: Barcode creation and formatting
6. **Database**: Location, item, and pick shift data storage

### Data Flow
1. User attempts to unassign location → System checks pick shift status
2. If item in active pick shift → Display "Unable to Unassign Location" message
3. Reserve label request → System retrieves item and location data
4. Label generation → Format data (Item, Barcode only)
5. Barcode generation → Transform location code (remove "-")

### Test Boundaries
- **Real Components**: UI messaging, label generation logic, barcode formatting
- **Mocked Components**: Pick shift service (if isolated testing required)
- **Integration Points**: Pick shift status check, label generation trigger

---

## 5. Feature and Business Rule Breakdown

### Feature 1: Location Unassignment During Active Pick Shift

#### Sub-Features
- Location unassignment validation
- UI message display
- Pick shift status integration

#### Business Rules
- BR-001: Item in active pick shift cannot have location unassigned
- BR-002: Message must display exact text from Figma specification
- BR-003: Message must be informative and user-friendly
- BR-004: User can unassign location after picking is complete

#### Field-Level Validations
- Location ID: Valid, exists in system
- Pick Shift Status: Active/Inactive
- Item ID: Valid, associated with location

#### State Transitions
```
[Location Assigned] → [Pick Shift Active] → [Location Unassignment Blocked]
                                          → [Message Displayed]
[Location Assigned] → [Pick Shift Complete] → [Location Unassignment Allowed]
```

### Feature 2: Reserve Label Generation

#### Sub-Features
- Label content formatting
- Barcode generation
- Label data retrieval

#### Business Rules
- BR-005: Reserve labels contain ONLY Item and Barcode
- BR-006: No additional item information (description, quantity, etc.) on label
- BR-007: Barcode represents location code
- BR-008: Barcode format excludes "-" character from location code

#### Field-Level Validations
- Item: Mandatory, valid item identifier
- Barcode: Mandatory, correctly formatted, scannable
- Location Code: Valid format, exists in system

#### Data Transformations
- Location Code Format: `ABC-123` → Barcode Format: `ABC123`

---

## 6. Coverage Model (Applied to Every Feature)

### 6.1 Functional Coverage

#### Happy Path Scenarios
- User attempts to unassign location during active pick shift → Message displayed correctly
- Reserve label generated with correct Item and Barcode fields
- Barcode scanned successfully matches location code (without "-")
- User successfully unassigns location after pick shift completes

#### Alternate Paths
- Multiple items in same location during pick shift
- Item in multiple pick shifts simultaneously
- Label generation for locations with various code formats

#### Negative Cases
- Attempt to unassign non-existent location
- Generate label with invalid location code
- Scan barcode with incorrect format
- Display message when pick shift status unavailable

### 6.2 Data Coverage

#### Equivalence Classes
- Location Codes:
  - Valid with hyphen: `ABC-123`, `LOC-456`
  - Valid without hyphen: `ABC123`, `LOC456`
  - Invalid formats: `ABC--123`, `123`, `ABC`
  
#### Boundary Values
- Location code length: Min, Max, Max+1
- Barcode character limits
- Item identifier length

#### Special Data Conditions
- Null location code
- Empty item identifier
- Location code with special characters
- Location code with only numbers
- Location code with only letters

### 6.3 State/Workflow Coverage

| Current State | Action | Expected Next State |
|---------------|--------|---------------------|
| Location Assigned, Pick Shift Active | Unassign Location | Message Displayed, State Unchanged |
| Location Assigned, Pick Shift Complete | Unassign Location | Location Unassigned |
| Location Assigned | Generate Reserve Label | Label Created with Item & Barcode |
| Label Generated | Scan Barcode | Barcode Recognized, Matches Location |

### 6.4 Role and Permission Coverage
- Warehouse Manager: Can attempt unassignment, receives message
- Warehouse Operator: Can generate labels
- System Administrator: Can override unassignment rules (if applicable)

### 6.5 Platform/API Version Coverage
- Web UI: Latest browser versions (Chrome, Firefox, Edge, Safari)
- Mobile UI: iOS and Android (if applicable)
- API versions: Current production API version

### 6.6 Integration Coverage

#### Success Scenarios
- Pick shift service returns active status → Message displays
- Label service receives location data → Label generates correctly
- Barcode generator processes location code → Barcode created

#### Failure Scenarios
- Pick shift service timeout → Error handling
- Label service unavailable → Graceful degradation
- Barcode generation fails → Error message displayed
- Database connection lost → Retry mechanism

### 6.7 Non-Functional Coverage
- **Performance**: Message displays within 1 second, Label generates within 2 seconds
- **Usability**: Message text is clear and actionable
- **Security**: Location data access properly authenticated
- **Accessibility**: Message readable by screen readers (WCAG 2.1 AA compliance)

---

## 7. Test Scenario Catalog

### 7.1 Happy Path Scenarios

#### TS-001: Display "Unable to Unassign Location" Message During Active Pick Shift
- **Scenario ID**: TS-001
- **Linked Requirement**: REQ-01, REQ-05
- **Preconditions**: Item exists, Location assigned, Pick shift active
- **Test Steps**:
  1. Navigate to location management interface
  2. Select location with item in active pick shift
  3. Attempt to unassign location
- **Expected Result**: 
  - Message displayed: "Unable to Unassign Location"
  - Subtitle: "This item is currently in a pick shift. You will be able to unassign this location once picking is complete."
  - Location remains assigned

#### TS-004: Generate Reserve Label with Only Item and Barcode
- **Scenario ID**: TS-004
- **Linked Requirement**: REQ-02
- **Preconditions**: Valid item, Valid location code
- **Test Steps**:
  1. Request reserve label generation
  2. Provide item identifier and location code
  3. Review generated label content
- **Expected Result**: 
  - Label contains exactly two fields: Item and Barcode
  - No additional information displayed

#### TS-007: Scan Successfully Generated Barcode
- **Scenario ID**: TS-007
- **Linked Requirement**: REQ-03
- **Preconditions**: Reserve label generated, Barcode scanner available
- **Test Steps**:
  1. Generate reserve label
  2. Use barcode scanner to scan the barcode
  3. Verify scanned value
- **Expected Result**: 
  - Barcode scans successfully on first attempt
  - Scanned value matches location code (without hyphen)

#### TS-010: Verify Barcode Format Matches Location Code Without Hyphen
- **Scenario ID**: TS-010
- **Linked Requirement**: REQ-04
- **Test Steps**:
  1. Input location code: `ABC-123`
  2. Generate reserve label
  3. Examine barcode value
- **Expected Result**: 
  - Barcode displays: `ABC123` (hyphen removed)
  - Barcode format is correct and scannable

### 7.2 Alternate Path Scenarios

#### TS-002: Verify Message Exactly Matches Figma Specification
- **Scenario ID**: TS-002
- **Linked Requirement**: REQ-01
- **Preconditions**: Figma specification accessible, Item in active pick shift
- **Test Steps**:
  1. Retrieve exact message text from Figma
  2. Trigger unassign location during active pick shift
  3. Compare displayed message with Figma specification
- **Expected Result**: 
  - Title matches exactly: "Unable to Unassign Location"
  - Body text matches exactly character-for-character
  - Formatting (font, size, color) matches Figma

#### TS-005: Generate Multiple Reserve Labels for Different Locations
- **Scenario ID**: TS-005
- **Linked Requirement**: REQ-02
- **Preconditions**: Multiple items with different locations
- **Test Steps**:
  1. Generate reserve label for Location A
  2. Generate reserve label for Location B
  3. Generate reserve label for Location C
  4. Verify each label content
- **Expected Result**: 
  - All labels contain only Item and Barcode
  - Each barcode corresponds to correct location code

#### TS-008: Scan Barcode from Different Label Formats/Sizes
- **Scenario ID**: TS-008
- **Linked Requirement**: REQ-03
- **Preconditions**: Labels printed in various sizes
- **Test Steps**:
  1. Generate small-sized label
  2. Generate medium-sized label
  3. Generate large-sized label
  4. Scan each barcode variant
- **Expected Result**: 
  - All barcode sizes scan successfully
  - Scanned values are identical and correct

### 7.3 Validation and Negative Scenarios

#### TS-003: Attempt Unassign Location When Pick Shift Status Unavailable
- **Scenario ID**: TS-003
- **Linked Requirement**: REQ-05
- **Preconditions**: Pick shift service unavailable or returns error
- **Test Steps**:
  1. Simulate pick shift service failure
  2. Attempt to unassign location
- **Expected Result**: 
  - System displays appropriate error message
  - Location unassignment prevented (fail-safe behavior)
  - OR System allows unassignment with warning (based on business rules)

#### TS-006: Verify No Extraneous Information on Reserve Label
- **Scenario ID**: TS-006
- **Linked Requirement**: REQ-02
- **Preconditions**: Item has rich metadata (description, quantity, weight, etc.)
- **Test Steps**:
  1. Select item with extensive details
  2. Generate reserve label
  3. Inspect label for any additional fields
- **Expected Result**: 
  - Label displays ONLY Item and Barcode
  - No description, quantity, weight, or other metadata visible

#### TS-009: Attempt to Scan Damaged or Partially Obscured Barcode
- **Scenario ID**: TS-009
- **Linked Requirement**: REQ-03
- **Preconditions**: Barcode with simulated damage or obstruction
- **Test Steps**:
  1. Generate reserve label
  2. Simulate barcode damage (smudge, partial tear)
  3. Attempt to scan barcode
- **Expected Result**: 
  - Barcode scanning fails gracefully
  - System provides clear error message
  - User can request label reprint

#### TS-011: Generate Barcode for Location Code Without Hyphen
- **Scenario ID**: TS-011
- **Linked Requirement**: REQ-04
- **Preconditions**: Location code format without hyphen (e.g., `ABC123`)
- **Test Steps**:
  1. Input location code: `ABC123` (no hyphen)
  2. Generate reserve label
  3. Verify barcode value
- **Expected Result**: 
  - Barcode displays: `ABC123` (unchanged)
  - Barcode scans correctly

#### TS-012: Verify Barcode for Location Code with Multiple Hyphens
- **Scenario ID**: TS-012
- **Linked Requirement**: REQ-04
- **Preconditions**: Location code with multiple hyphens (e.g., `AB-CD-123`)
- **Test Steps**:
  1. Input location code: `AB-CD-123`
  2. Generate reserve label
  3. Verify barcode value
- **Expected Result**: 
  - Barcode displays: `ABCD123` (all hyphens removed)
  - Barcode scans correctly

### 7.4 Authorization and Edge Cases

#### TS-013: Verify Location Unassignment After Pick Shift Completion
- **Scenario ID**: TS-013
- **Linked Requirement**: REQ-05
- **Preconditions**: Item previously in active pick shift, Pick shift now complete
- **Test Steps**:
  1. Complete active pick shift
  2. Attempt to unassign location
- **Expected Result**: 
  - Location unassignment succeeds
  - No blocking message displayed
  - Location status updated to unassigned

#### TS-014: Verify Message NOT Displayed When Pick Shift Inactive
- **Scenario ID**: TS-014
- **Linked Requirement**: REQ-05
- **Preconditions**: Item exists, No active pick shift for item
- **Test Steps**:
  1. Navigate to location management
  2. Select location without active pick shift
  3. Unassign location
- **Expected Result**: 
  - Location unassigned successfully
  - "Unable to Unassign Location" message NOT displayed
  - Confirmation of successful unassignment shown

---

## 8. Test Data Strategy

### Required Data Sets

#### Valid Data
- **Location Codes**:
  - `ABC-123` (standard format with hyphen)
  - `LOC-456` (alternate format)
  - `WH1-789` (numeric suffix)
  - `A-1` (minimal length)
  - `WAREHOUSE-12345` (extended length)

- **Items**:
  - Standard item with all metadata
  - Item with minimal information
  - Item with special characters in name

- **Pick Shifts**:
  - Active pick shift (status: In Progress)
  - Completed pick shift (status: Complete)
  - Cancelled pick shift (status: Cancelled)

#### Invalid Data
- **Location Codes**:
  - Empty string
  - Null value
  - Special characters only: `@#$%`
  - Excessively long code (beyond system limit)
  - Location code with spaces: `ABC - 123`

#### Edge Case Data
- Location code exactly at character limit
- Location code with consecutive hyphens: `ABC--123`
- Location code with leading/trailing hyphens: `-ABC-123-`
- Numeric-only location code: `12345`
- Alpha-only location code: `ABCDEF`

### Test Users and Roles
- Warehouse Manager (full permissions)
- Warehouse Operator (label generation, limited unassignment)
- Read-Only User (view only, cannot unassign or generate)

### Data Setup Approach
1. Pre-populate test database with controlled location and item data
2. Create test pick shifts for specific scenarios
3. Use data builder scripts for repeatable setup
4. Implement cleanup scripts to restore test state

### Data Cleanup
- Delete test pick shifts after test execution
- Reset location assignments to default state
- Archive generated test labels
- Maintain audit trail for traceability

---

## 9. Test Environment and Configuration

### Test Environments

#### Environment 1: Integration Test Environment
- **Purpose**: Feature validation, integration testing
- **Configuration**: 
  - Connected to test pick shift service
  - Mock barcode scanner (virtual scanning)
  - Label generation service (test mode)
- **Data**: Dedicated test dataset

#### Environment 2: UAT Environment
- **Purpose**: User acceptance testing, Figma validation
- **Configuration**:
  - Production-like setup
  - Real barcode scanning capability
  - Physical label printer
- **Data**: Sanitized production data subset

### Feature Flags
- `enable_new_unassign_message`: ON (to enable updated UI message)
- `reserve_label_minimal_info`: ON (to show only Item and Barcode)

### Stubs and Mocks
- Mock Pick Shift Service: Returns predefined active/inactive status
- Mock Barcode Generator: Validates format without physical generation
- Stub Label Printer: Simulates label output for format verification

### Versioning Assumptions
- Application Version: v2.5.0 (post-demo requirement changes)
- API Version: v3.1
- Database Schema: v1.8

---

## 10. Entry and Exit Criteria

### Entry Criteria
1. ✅ Figma design specifications finalized and accessible
2. ✅ Test environment provisioned with required services
3. ✅ Test data prepared and loaded
4. ✅ Barcode scanning capability available (physical or virtual)
5. ✅ All prerequisite features (pick shift management) functional
6. ✅ Test Plan reviewed and approved

### Exit Criteria
1. ✅ 100% Requirements Traceability Matrix coverage executed
2. ✅ All 14 test scenarios executed successfully
3. ✅ Zero critical or high-severity defects open
4. ✅ UI message validated against Figma (exact match confirmed)
5. ✅ Barcode scannability verified at 100% success rate
6. ✅ All test results documented and reviewed
7. ✅ Regression testing completed for impacted features
8. ✅ Sign-off obtained from Product Owner and QA Lead

---

## 11. Defect Management

### Severity Definitions

| Severity | Description | Example |
|----------|-------------|---------|
| Critical | System crash, data loss, security breach | Application crashes when unassigning location |
| High | Core functionality broken, no workaround | Message text does not match Figma, barcode unscannable |
| Medium | Functionality impaired, workaround exists | Message formatting incorrect, barcode scans on retry |
| Low | Cosmetic issue, minor inconvenience | Message alignment off by 2px |

### Priority Definitions
- **P0**: Fix immediately, blocks testing
- **P1**: Fix before release
- **P2**: Fix in next sprint
- **P3**: Fix when time permits

### Retest Rules
- All Critical and High defects: Retest after fix + regression test
- Medium defects: Retest after fix
- Low defects: Verify in next regression cycle

### Regression Scope
- Location unassignment for items NOT in pick shifts (existing functionality)
- Pick shift creation and management (integration point)
- Standard label generation (non-reserve labels)

### Stop-Ship Criteria
Testing cannot proceed OR release cannot happen if:
- UI message does not match Figma specification
- Barcode scannability below 95%
- Location can be unassigned during active pick shift (critical defect)
- More than 2 high-severity defects open

---

## 12. Test Levels and Types

### Test Types Coverage

| Test Type | Scope | Test Scenario IDs | Automation |
|-----------|-------|-------------------|------------|
| **Functional** | Core functionality validation | TS-001, TS-004, TS-007, TS-010, TS-013 | Manual |
| **UI/UX** | Message display, Figma validation | TS-002 | Manual |
| **Integration** | Pick shift service, label service | TS-001, TS-003, TS-004 | Automated |
| **Negative** | Invalid inputs, error handling | TS-003, TS-006, TS-009 | Automated |
| **Edge Case** | Boundary values, special formats | TS-011, TS-012 | Manual |
| **Regression** | Existing functionality unaffected | TS-014 + Previous test suite | Automated |
| **Smoke** | Critical path validation | TS-001, TS-007 | Automated |
| **End-to-End** | Complete workflow | TS-001 → TS-013 (pick shift lifecycle) | Manual |

### Manual vs Automated Testing

#### Manual Testing Scope
- Figma visual validation (TS-002)
- Physical barcode scanning (TS-007, TS-008)
- Label content inspection (TS-004, TS-006)
- User experience validation

#### Automated Testing Scope
- API integration testing (pick shift status)
- Barcode format validation (TS-010, TS-011, TS-012)
- Negative test scenarios (TS-003)
- Regression suite
- Data-driven tests (multiple location code formats)

---

## 13. Risk-Based Testing

### High-Risk Areas

#### Risk 1: UI Message Mismatch with Figma
- **Impact**: High (user confusion, non-compliance with design)
- **Probability**: Medium
- **Mitigation**: 
  - Mandatory test: TS-002 (exact character validation)
  - QA-Designer paired review before release
  - Screenshot comparison automated check

#### Risk 2: Barcode Unscannability
- **Impact**: Critical (operational disruption, warehouse delays)
- **Probability**: Low
- **Mitigation**: 
  - Mandatory tests: TS-007, TS-008, TS-009
  - Test with multiple physical scanners
  - Validate barcode generation library compliance
  - Test various label sizes and print qualities

#### Risk 3: Location Unassigned During Active Pick Shift
- **Impact**: Critical (data integrity, picking errors)
- **Probability**: Low
- **Mitigation**: 
  - Mandatory tests: TS-001, TS-003, TS-013
  - Integration test with real pick shift service
  - Negative testing for service failures
  - Database constraint validation

#### Risk 4: Additional Information Leaking onto Reserve Label
- **Impact**: Medium (privacy concern, label clutter)
- **Probability**: Medium
- **Mitigation**: 
  - Mandatory tests: TS-004, TS-006
  - Test with items having extensive metadata
  - Code review of label template
  - Visual inspection of generated labels

### Mandatory Tests Per Risk
- **Risk 1**: TS-002 (must pass)
- **Risk 2**: TS-007, TS-008 (must pass, 100% scan success)
- **Risk 3**: TS-001, TS-013 (must pass, zero data integrity issues)
- **Risk 4**: TS-006 (must pass, zero extraneous fields)

---

## 14. Approvals and Sign-Off

### Test Plan Review
- **QA Lead**: [Name] - Review and approval required
- **Product Owner**: [Name] - Business requirements validation
- **Development Lead**: [Name] - Technical feasibility confirmation
- **UX Designer**: [Name] - Figma specification alignment

### Test Execution Sign-Off
- **Test Executor**: [Name] - Confirms all scenarios executed
- **QA Lead**: [Name] - Confirms exit criteria met
- **Product Owner**: [Name] - Accepts deliverable for release

---

## Appendix

### Glossary
- **Pick Shift**: A scheduled period during which items are picked from locations for order fulfillment
- **Reserve Label**: A label used to identify reserved inventory locations
- **Location Code**: Unique identifier for a physical warehouse location
- **RTM**: Requirements Traceability Matrix

### References
- Figma Design Specification: [Link to Figma]
- Requirement Document: `requirement.md`
- Pick Shift Management API Documentation: [Link]
- Barcode Standards: Code 128, Code 39 (specify applicable standard)

### Test Scenario Summary
- Total Test Scenarios: 14
- Happy Path: 4
- Alternate Path: 4
- Negative/Validation: 4
- Edge Cases: 2

---

**Document Version**: 1.0  
**Created Date**: February 12, 2026  
**Last Updated**: February 12, 2026  
**Status**: Active
