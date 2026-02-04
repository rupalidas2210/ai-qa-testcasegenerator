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

#### 2.3 CSV Format Requirements
- Convert test scenarios from the Test Plan into structured test cases.
- Generate test cases using ZephyrTestCaseTemplate.csv
- Each test case must start on a single row with all test metadata populated:

  Name, Objective, Pre-condition, Test Step (Step 1), Test Data, Test Result, Labels, Components, Parent Link, QA Engineer, Fix versions, Affect versions, Automated, API, Jira, Sub Domain.

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

---

### 3. File Naming Convention
- Extract the project name from the Test Plan file name
- Format the output file name as: ProjectName_Zephyrimportready.csv
- **Save location**: `.github\agents\Test Case Generator\agents-context\Test Case\ZephyrReadyTestCases\`
- **Full path example**: `.github\agents\Test Case Generator\agents-context\Test Case\ZephyrReadyTestCases\Spectrum_Brand_Manager_Zephyrimportready.csv`
- Example: If Test Plan is "Spectrum_Brand_Manager_TestPlan.md", CSV file should be "Spectrum_Brand_Manager_Zephyrimportready.csv"

---

### 4. Response Format
- Respond with the project name followed by "Zephyrimportready.csv created in .github\agents\Test Case Generator\agents-context\skills\Test Case\ZephyrReadyTestCases"
- Include summary of test case types generated
- Example response:
  ```
  # Spectrum Brand Manager - Zephyrimportready.csv created in .github\agents\Test Case Generator\agents-context\skills\Test Case\ZephyrReadyTestCases
  
  ✅ Test Cases Generated: 65 test cases covering:
     - Functional: 25 test cases
     - Regression: 10 test cases
     - Smoke: 5 test cases
     - E2E: 8 test cases
     - Integration: 7 test cases
     - Negative: 6 test cases
     - Edge: 4 test cases
  ```
