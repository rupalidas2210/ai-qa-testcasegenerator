---
name : Generate Zephyr Test Case
Description : A skill that converts a Test Plan into Zephyr-ready CSV test cases with complete coverage of all test types
---

# Generate Zephyr Test Case
A skill that converts a Test Plan into Zephyr-ready CSV test cases with complete coverage of all test types.
This skill reads an existing Test Plan and generates structured test cases in CSV format ready for import into Zephyr.

## Workflow: Test Plan → Zephyr Import Test Cases

### 1. Read the Test Plan File
- Locate and read the Test Plan file from `.github\agents\Test Case Generator\agents-context\Test Case\TestPlan\`
- Parse all test scenarios, requirements traceability, and coverage requirements
- Extract project name from the Test Plan
- Understand all functional requirements, business rules, and acceptance criteria


### 2. Generate Zephyr Ready Import Test Cases

#### 2.1 Test Case Types - MANDATORY Coverage
Generate test cases for **ALL** of the following types:

##### 2.1.1 Functional Test Cases
- Verify each feature works as per requirements
- Cover all positive workflows
- Validate business logic and acceptance criteria

##### 2.1.2 Regression Test Cases
- Verify existing functionality after changes
- Cover critical user journeys end-to-end
- Include previously fixed defects

##### 2.1.3 Smoke Test Cases
- Quick validation of critical paths
- Verify system is stable for further testing
- Cover login, core features, basic workflows
- Priority: P0

##### 2.1.4 End-to-End (E2E) Test Cases
- Complete user journeys across multiple components
- Integration of UI → Backend → Database → External Systems
- Real-world scenarios with full data flow
- Priority: P0/P1

##### 2.1.5 Integration Test Cases
- Verify communication between modules/services
- API integrations with external systems
- Database interactions
- Message queue/event processing
- Priority: P1

##### 2.1.6 Negative Test Cases
- Invalid inputs (empty, null, special characters)
- Boundary violations (max length, limits exceeded)
- Unauthorized access attempts
- Invalid state transitions
- Malformed API requests
- Priority: P1/P2

##### 2.1.7 Edge Test Cases
- Boundary values (min/max)
- Concurrent users/requests
- Large data sets
- Network failures/timeouts
- System limits (pagination, batch sizes)
- Race conditions
- Priority: P2

#### 2.2 Test Case Distribution Guidelines
- **Functional**: 30-40% of total test cases
- **Regression**: 15-20% of total test cases
- **Smoke**: 5-10% of total test cases
- **E2E**: 10-15% of total test cases
- **Integration**: 10-15% of total test cases
- **Negative**: 15-20% of total test cases
- **Edge**: 10-15% of total test cases

#### 2.3 CSV Format Requirements - MANDATORY TEMPLATE ENFORCEMENT

**CRITICAL: Strict Template Compliance Required**

**Template Location (READ THIS FILE FIRST):**
- **Mandatory Template Path:** `.github\agents\Test Case Generator\agents-context\skills\Test Case\Template\ZephyrTestCaseTemplate.csv`
- **You MUST read this template file before generating any CSV**
- **The template contains the EXACT column headers that MUST be used**

**MANDATORY Column Headers (In Exact Order):**
The generated CSV MUST contain these 16 columns in this exact order:

1. Name
2. Objective
3. Pre-condition
4. Test Step
5. Test Data
6. Test Result
7. Labels
8. Components
9. QA Engineer
10. Fix versions
11. Affect versions
12. Automated
13. API
14. Jira
15. Sub Domain
16. Requirement ID


**CSV Generation Rules:**
- Convert test scenarios from the Test Plan into structured test cases using ONLY the template columns
- Each test case must start on a single row with all test metadata populated in the template columns

- **IMPORTANT:** The "Sub Domain" column must always be left blank (empty) for all test cases.
- If a test case has more than one step:
  - Step 1 must appear in the main test case row under the "Test Step" column
  - Step 2, Step 3, and subsequent steps must each appear on their own new rows beneath Step 1 under the "Test Step" column

- For Step 2+ rows:
  - Only the "Test Step" column should contain text.
  - All other columns must be left blank.

- Do NOT merge steps into a single row.
- Do NOT place steps in the "Test Data" column.
- Preserve step numbering exactly as:

  Step 1:
  Step 2:
  Step 3:

#### 2.4 Labels Column - Test Type Identification
Each test case MUST have appropriate labels in the "Labels" column:
- Functional test cases: Add label "Functional"
- Regression test cases: Add label "Regression"
- Smoke test cases: Add label "Smoke"
- E2E test cases: Add label "E2E"
- Integration test cases: Add label "Integration"
- Negative test cases: Add label "Negative"
- Edge test cases: Add label "Edge"

**IMPORTANT - Multiple Labels Formatting:**
- Multiple labels MUST be placed in the SAME "Labels" column cell
- Separate multiple labels with commas and NO spaces
- Example: `Functional,Regression,E2E` (all in one cell)
- Do NOT spread labels across multiple columns
- Correct format in CSV: `"Functional,Regression,E2E"` in the Labels column
- Incorrect: Having Functional in one column, Regression in another column

#### 2.5 Requirement ID Column - Requirements & Test Scenario Traceability
The "Requirement ID" column MUST contain ONE Requirement ID and ONE Test Scenario ID per test case:

**How to Extract from RTM:**
- **Always reference the RTM table (Section 3) in the Test Plan**
- For each test case, look up the corresponding row in the RTM
- Extract the Requirement ID (Req ID column) and ONE Test Scenario ID (from Test Scenario IDs column)
- Create separate test cases for each Test Scenario ID listed in the RTM

**RTM Example:**
```
| Req ID  | Requirement Description        | Acceptance Criteria | Test Scenario IDs | Test Case IDs |
|---------|--------------------------------|---------------------|-------------------|---------------|
| REQ-001 | Login Screen UI Elements       | Display User ID...  | TS-001, TS-002    | TBD           |
```

**This RTM row generates TWO test cases:**
- **Test Case 1** - Requirement ID column: `"REQ-001,TS-001"` (quoted in CSV)
- **Test Case 2** - Requirement ID column: `"REQ-001,TS-002"` (quoted in CSV)

**CRITICAL - One-to-One Mapping Rule:**
- Each test case = ONE Requirement ID + ONE Test Scenario ID
- Format in CSV file: `"REQ-XXX,TS-YYY"` (comma-separated values MUST be wrapped in quotes)
- If RTM shows multiple Test Scenario IDs for one Requirement, create separate test cases for EACH scenario
- Do NOT combine multiple Test Scenario IDs in one test case

**Formatting Rules:**
- Both Requirement ID and Test Scenario ID MUST be in the SAME "Requirement ID" column cell
- Do NOT create a second column for TS- values
- **ALWAYS wrap the value in double quotes when writing to CSV:** `"REQ-001,TS-001"`
- Without quotes, the comma will be treated as a column separator
- **Same rule as Labels column:** Just like `"Functional,Regression,E2E"` must be quoted, so must `"REQ-001,TS-001"`

**Requirements Traceability Best Practices:**
- Every test case must have exactly ONE REQ ID and ONE TS ID from the RTM in the same Requirement ID column cell
- Do NOT create a second column for TS ID
- Format: `"REQ-XXX,TS-YYY"` (quoted, comma-separated, no spaces)
- If RTM shows `TS-001, TS-002`, create two separate test cases with separate rows
- Maintain one-to-one traceability: 1 Requirement ID ↔ 1 Test Scenario ID ↔ 1 Test Case
- Ensure 100% RTM coverage by creating test cases for all test scenarios listed
- **Verify in the generated CSV that Requirement ID values appear in a SINGLE column, not split across two columns**
- Cross-verify each test case maps back to correct row in RTM table

#### 2.6 Sub Domain Column - Leave Blank
**MANDATORY Rule:**
- The "Sub Domain" column MUST always be left blank (empty) for all test cases
- Do NOT populate this column with any values
- This applies to both the main test case row and all subsequent step rows
- Format in CSV: Leave the Sub Domain column empty with no text

### 3. File Naming Convention
- Extract the project name from the Test Plan file name
- Format the output file name as: ProjectName_Zephyrimportready.csv
- **Save location**: `.github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases\`
- **Full path example**: `.github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases\Spectrum_Brand_Manager_Zephyrimportready.csv`
- Example: If Test Plan is "Spectrum_Brand_Manager_TestPlan.md", CSV file should be "Spectrum_Brand_Manager_Zephyrimportready.csv"

### 3.1 Pre-Generation Template Validation (MANDATORY)
**Before generating any CSV file, you MUST:**

1. **Read the Template File:**
   ```
   Path: .github\agents\Test Case Generator\agents-context\skills\Test Case\Template\ZephyrTestCaseTemplate.csv
   ```

2. **Extract Template Headers:**
   - Read line 1 of the template
   - Store the exact column headers
   - Count must equal 16 columns

3. **Use Template Headers in Output:**
   - Use the extracted headers as the first row of your generated CSV
   - Do NOT hardcode headers
   - Do NOT add, remove, or modify any column headers

4. **Validation Check:**
   - After generation, verify your CSV has exactly 16 columns
   - Verify the header row matches the template exactly
   - If validation fails: DO NOT save the file and report the error

**Example Validation Logic:**
```
IF generated_csv_headers != template_headers THEN
    ERROR: "CSV does not match ZephyrTestCaseTemplate.csv format"
    ERROR: "Expected 16 columns, got X columns"
    ERROR: "Missing columns: [list]"
    ERROR: "Extra columns: [list]"
    ABORT: Do not save the file
END IF
```

---

### 4. Response Format
- Respond with the project name followed by "Zephyrimportready.csv created in .github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases"
- **MANDATORY: Include template validation confirmation**
- Include summary of test case types generated
- Example response:
  ```
  # Spectrum Brand Manager - Zephyrimportready.csv created in .github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases
  
  ✅ Template Validation: PASSED
     - Using ZephyrTestCaseTemplate.csv (16 columns)
     - All headers match template exactly
  
  ✅ Test Cases Generated: 65 test cases covering:
     - Functional: 25 test cases
     - Regression: 10 test cases
     - Smoke: 5 test cases
     - E2E: 8 test cases
     - Integration: 7 test cases
     - Negative: 6 test cases
     - Edge: 4 test cases
  ```
  
### 5. Quality Checklist (MUST VERIFY BEFORE COMPLETING)
Before reporting completion, verify:
- [ ] Template file was read from correct path
- [ ] Generated CSV has exactly 16 columns
- [ ] Column headers match template exactly (case-sensitive)
- [ ] No extra columns added (like Priority, Owner, Status, etc.)
- [ ] No columns removed or renamed
- [ ] Sub Domain column is empty for all rows
- [ ] File saved to correct location: `.github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases\`
