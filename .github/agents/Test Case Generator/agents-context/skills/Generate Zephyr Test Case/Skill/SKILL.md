---
name : Generate Zephyr Test Case
Description : A skill that converts a Test Plan into Zephyr-ready CSV test cases with complete coverage of all test types
---

# Generate Zephyr Test Case
A skill that converts a Test Plan into Zephyr-ready CSV test cases with complete coverage of all test types.
This skill reads an existing Test Plan and generates structured test cases in CSV format ready for import into Zephyr.

---

Before generating ANY CSV file, you MUST:

1. **READ the template file:**
   ```
   Path:.github\agents\Test Case Generator\agents-context\skills\Test Case\Template\ZephyrTestCaseTemplate.csv
   ```

2. **EXTRACT the exact column headers** from line 1 of the template

3. **USE ONLY those 16 columns** - Do NOT add, remove, or modify ANY columns

4. **VALIDATE** your generated CSV matches the template exactly before saving

**❌ FORBIDDEN COLUMNS (NOT in template):**
- Priority, Status, Owner, Folder, Estimated Time, Test Script Type, Component (without 's'), Precondition (without hyphen), Expected Result

**✅ REQUIRED COLUMNS (From template - exactly 16):**
- Name, Objective, Pre-condition, Test Step, Test Data, Test Result, Labels, Components, QA Engineer, Fix versions, Affect versions, Automated, API, Jira, Sub Domain, Requirement ID

**Template validation is MANDATORY before saving any CSV file.**

---
## 🔴 QUICK REFERENCE: Avoiding Column Splitting Issues

**Problem:** Commas in cell values create extra columns (16 becomes 17+)

**Solution:** Wrap comma-containing values in double quotes

**Critical Columns That MUST Have Quotes:**
1. **Labels (Column 7)**: `"Functional,Regression,E2E"` 
2. **Requirement ID (Column 16)**: **`"REQ-001,TS-001"`** ← Most critical!

**⚠️ Why Requirement ID Always Creates 17 Columns Without Quotes:**
- Writing `REQ-001,TS-001` without quotes: CSV sees comma as delimiter
- Result: REQ-001 in column 16, TS-001 in column 17 ❌
- Fix: **Always write `"REQ-001,TS-001"` with quotes** ✅

**Validation Check:**
- Count columns in every row = Must be exactly 16
- **If you see 17 columns, check Requirement ID column for missing quotes**
- The comma in `REQ-XXX,TS-YYY` MUST be wrapped in quotes

---

## Workflow: Test Plan → Zephyr Import Test Cases

### 1. Read the Test Plan File
- Locate and read the Test Plan file from `.github\agents\Test Case Generator\agents-context\Test Case\TestPlan\`
- Parse all test scenarios, requirements traceability, and coverage requirements
- Extract project name from the Test Plan
- Understand all functional requirements, business rules, and acceptance criteria


### 2. Generate Zephyr Ready Import Test Cases

**🔴 BEFORE STARTING: READ THE TEMPLATE FILE FIRST**
```
MANDATORY FIRST ACTION:
1. Read: .github\agents\Test Case Generator\agents-context\skills\Test Case\Template\ZephyrTestCaseTemplate.csv
2. Extract: The exact column headers from line 1
3. Use: ONLY those 16 columns for your CSV generation
4. Validate: Confirm you have exactly 16 columns before proceeding
```

**🚨 CRITICAL CSV FORMATTING RULE - PREVENTS 17 COLUMN ERROR:**

**When a cell contains commas, wrap it in double quotes:**
- Labels: `"Functional,Regression,E2E"`
- Requirement ID: **`"REQ-001,TS-001"`** ← THIS IS THE MOST COMMON MISTAKE!

**Why?** Without quotes, CSV treats commas as column separators.

**Example - Requirement ID Column:**
```csv
❌ WRONG (17 columns): ...,REQ-001,TS-001
                            ↑col16  ↑col17 (split by comma)

✅ CORRECT (16 columns): ...,"REQ-001,TS-001"
                             ↑col16 (one value)
```

**When generating CSV rows:**
- Always write: `"REQ-001,TS-001"` with quotes
- Never write: `REQ-001,TS-001` without quotes
- The comma MUST be inside the quotes to stay in one column

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

**⚠️ CRITICAL: ABSOLUTE TEMPLATE COMPLIANCE REQUIRED - NO EXCEPTIONS ⚠️**

**🔴 STEP 1 - READ TEMPLATE FILE FIRST (MANDATORY):**
Before generating ANY CSV content, you MUST:
1. **Read the template file:** `.github\agents\Test Case Generator\agents-context\skills\Test Case\Template\ZephyrTestCaseTemplate.csv`
2. **Extract the exact header row** from line 1 of the template
3. **Use ONLY those column headers** - do not add, remove, or modify ANY columns
4. **Copy the header row exactly** as the first line of your generated CSV

**Template Location:**
```
MANDATORY PATH: .github\agents\Test Case Generator\agents-context\skills\Test Case\Template\ZephyrTestCaseTemplate.csv
```

**🔴 VALIDATION CHECKPOINT:**
After reading the template, verify you have exactly **16 columns** in this exact order:
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

**❌ FORBIDDEN - DO NOT USE THESE COLUMNS:**
- Priority (not in template)
- Component (different from "Components")
- Status (not in template)
- Owner (different from "QA Engineer")
- Folder (not in template)
- Estimated Time (not in template)
- Test Script Type (not in template)
- Precondition (different from "Pre-condition" with hyphen)
- Expected Result (different from "Test Result")

**✅ CSV Generation Rules:**
- **First line of CSV:** Copy the exact header row from the template file
- **Do NOT hardcode headers** - always read them from the template
- Each test case row must use ONLY the 16 template columns
- Fill appropriate columns with test case data, leave others blank if not applicable

**Multi-Step Test Cases Formatting:**
- **IMPORTANT:** The "Sub Domain" column must always be left blank (empty) for all test cases
- If a test case has multiple steps:
  - **Row 1 (Main test case row):** Populate all metadata columns (Name, Objective, Pre-condition, Labels, etc.) + Step 1 in "Test Step" column
  - **Row 2:** Leave all columns blank EXCEPT "Test Step" column (contains Step 2)
  - **Row 3:** Leave all columns blank EXCEPT "Test Step" column (contains Step 3)
  - Continue pattern for all additional steps

- For Step 2+ rows:
  - Only the "Test Step" column should contain text
  - All other 15 columns must be completely blank (empty cells)

- Do NOT merge steps into a single row
- Do NOT place steps in the "Test Data" column
- Preserve step numbering format:
  ```
  Step 1: [description]
  Step 2: [description]
  Step 3: [description]
  ```

#### 2.4 Labels Column - Test Type Identification

**Labels to use:**
- Functional, Regression, Smoke, E2E, Integration, Negative, Edge

**Format for multiple labels:**
- Combine in ONE cell: `"Functional,Regression,E2E"`
- **MUST wrap in double quotes** to prevent comma from splitting into extra columns
- No spaces after commas

**Examples:**
```csv
✅ CORRECT: "Functional,Regression,E2E"
❌ WRONG: Functional,Regression,E2E  (creates 3 columns instead of 1)
```

#### 2.5 Requirement ID Column - Requirements & Test Scenario Traceability

**🔴 CRITICAL FORMATTING RULE - READ CAREFULLY:**

The "Requirement ID" column (last column, #16) contains BOTH values in a SINGLE cell:
- Format: **`"REQ-XXX,TS-YYY"`** (MUST include double quotes)
- **WITHOUT quotes, the comma is treated as a CSV delimiter and splits into 2 columns**
- Example: `"REQ-001,TS-001"`

**🚨 WHY QUOTES ARE MANDATORY:**
In CSV format, commas separate columns. When you write `REQ-001,TS-001` without quotes:
- CSV parser sees: column 16 = `REQ-001`, column 17 = `TS-001` ❌
- Result: 17 columns total (breaks import)

When you write `"REQ-001,TS-001"` with quotes:
- CSV parser sees: column 16 = `REQ-001,TS-001` (one value) ✅
- Result: 16 columns total (correct)

**❌ WRONG - Creates 17 columns:**
```csv
...,,,,,REQ-001,TS-001
       ↑col 16 ↑col 17 (BROKEN - two columns created)
```

**✅ CORRECT - 16 columns:**
```csv
...,,,,,"REQ-001,TS-001"
       ↑col 16 (one column with both values)
```

**How to Extract from Test Plan RTM:**
1. Find the test scenario in the RTM (Requirements Traceability Matrix)
2. Get the Requirement ID from the "Req ID" column
3. Get ONE Test Scenario ID from the "Test Scenario IDs" column
4. Combine as: **`"REQ-XXX,TS-YYY"`** with quotes in the Requirement ID column

**If RTM shows multiple scenarios:**
- RTM: `REQ-001` with scenarios `TS-001, TS-002`
- Create 2 separate test case rows:
  - Row 1: **`"REQ-001,TS-001"`** (quoted)
  - Row 2: **`"REQ-001,TS-002"`** (quoted)

**⚠️ CRITICAL VALIDATION:**
- Every CSV row must have exactly 16 columns
- **If you see 17 columns, you forgot quotes around `"REQ-XXX,TS-YYY"`**
- The comma between REQ and TS MUST be inside quotes to prevent column splitting
- When writing CSV: Always use `"REQ-001,TS-001"` NOT `REQ-001,TS-001`

#### 2.6 Sub Domain Column - Leave Blank
**MANDATORY Rule:**
- The "Sub Domain" column MUST always be left blank (empty) for all test cases
- Do NOT populate this column with any values
- This applies to both the main test case row and all subsequent step rows
- Format in CSV: Leave the Sub Domain column empty with no text

---

### 2.7 CSV ROW FORMAT EXAMPLES

**🔴 CRITICAL: All examples show `"REQ-XXX,TS-YYY"` in QUOTES - this is mandatory!**

**Single-Step Test Case (16 columns):**
```csv
"TC-001: Test Name","Test objective","Pre-conditions","Step 1: Action","Test data","Expected result","Functional,Smoke","Component",,,,,No,,,,"REQ-001,TS-001"
```
**Column breakdown:** 1=Name, 2=Objective, 3=Pre-condition, 4=Test Step, 5=Test Data, 6=Test Result, 7=Labels(quoted), 8=Components, 9-15=empty, 16=**RequirementID(quoted)**

**❌ WRONG - Without quotes (creates 17 columns):**
```csv
"TC-001: Test","Objective",...,No,,,REQ-001,TS-001
                                   ↑col16 ↑col17 (BROKEN)
```

**Multi-Step Test Case (Main row + continuation rows):**
```csv
"TC-002: Multi-Step","Objective","Pre-conditions","Step 1: First action","Data 1","Result 1","Functional","Component",,,,,No,,,,"REQ-002,TS-005"
,,,"Step 2: Second action","Data 2","Result 2",,,,,,,,,,
,,,"Step 3: Third action","Data 3","Result 3",,,,,,,,,,
```
*Note: `"REQ-002,TS-005"` with quotes in column 16 of row 1; Continuation rows have 13 empty + 3 filled*

**Multiple Test Scenarios from Same Requirement:**
```csv
"TC-010: Scenario A","Objective A","Pre-cond A","Step 1","Data A","Result A","Functional",,,,,No,,,,"REQ-004,TS-010"
"TC-011: Scenario B","Objective B","Pre-cond B","Step 1","Data B","Result B","Negative",,,,,No,,,,"REQ-004,TS-011"
```
*Note: Each row has `"REQ-004,TS-XXX"` quoted in column 16; Same REQ, different TS = separate rows*

---

### 3. File Naming Convention
- Extract the project name from the Test Plan file name
- Format the output file name as: ProjectName_Zephyrimportready.csv
- **Save location**: `.github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases\`
- **Full path example**: `.github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases\Spectrum_Brand_Manager_Zephyrimportready.csv`
- Example: If Test Plan is "Spectrum_Brand_Manager_TestPlan.md", CSV file should be "Spectrum_Brand_Manager_Zephyrimportready.csv"

---

### 4. Pre-Generation Template Validation (MANDATORY - EXECUTE THESE STEPS)

**🔴 CRITICAL: Follow these steps IN ORDER before generating CSV:**

**STEP 1: Read Template File**
```
Action: Read file at path: .github\agents\Test Case Generator\agents-context\skills\Test Case\Template\ZephyrTestCaseTemplate.csv
Required: Read lines 1-2 (header + any example row if present)
Store: Extract the complete first line (header row)
```

**STEP 2: Parse Template Headers**
- Split the header row by commas
- Store each column header exactly as it appears (preserve case, spacing, hyphens)
- Count total columns (must equal 16)
- Create ordered list: [column1, column2, ..., column16]

**STEP 3: Validate Template Structure**
```
✅ MUST HAVE: Exactly 16 columns
✅ REQUIRED COLUMNS: Name, Objective, Pre-condition, Test Step, Test Data, Test Result, Labels, Components, QA Engineer, Fix versions, Affect versions, Automated, API, Jira, Sub Domain, Requirement ID
❌ ABORT IF: Column count ≠ 16
❌ ABORT IF: Any required column is missing
```

**STEP 4: Generate CSV with Template Headers**
- **Line 1 of output CSV:** Copy the exact header row from template (character-for-character match)
- **Line 2+:** Test case data rows using only the 16 template columns
- **NO custom columns allowed** - only use what's in the template

**STEP 5: Post-Generation Validation**
After creating the CSV content, validate:
```
CHECK 1: First line of generated CSV matches template header exactly
CHECK 2: Every data row has exactly 16 column values (some may be blank)
CHECK 3: No column headers have been added, removed, or modified
CHECK 4: "Sub Domain" column is blank for all rows
CHECK 5: All test case rows follow the template structure

IF ANY CHECK FAILS:
  - DO NOT save the file
  - Report the specific validation error
  - Show expected vs actual headers
  - Request correction before proceeding
```

**STEP 6: Final Verification Before Save**
```
Before calling create_file or write_file:
  ✓ Template file was read successfully
  ✓ Headers extracted and validated
  ✓ Generated CSV uses exact template headers
  ✓ All 16 columns present in every row
  ✓ No extra or missing columns
  ✓ Multi-step test cases formatted correctly
  ✓ "Sub Domain" column left blank throughout
```

**❌ VALIDATION FAILURE PROTOCOL:**
```
IF validation fails:
  1. STOP immediately - do not save file
  2. Report error message:
     "❌ CSV GENERATION FAILED - Template validation error"
     "Expected: [template headers]"
     "Generated: [your headers]"
     "Mismatch: [specific differences]"
  3. Do not proceed until issue is resolved
```

---

### 5. Response Format
After successful CSV generation and validation, respond with:

**Required Response Structure:**
```markdown
# [Project Name] - Zephyrimportready.csv created in .github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases

✅ TEMPLATE VALIDATION: PASSED
   - Template Source: ZephyrTestCaseTemplate.csv
   - Columns Validated: 16/16 columns match
   - Headers Match: 100% exact match
   - Format Compliance: ✅ Complete

✅ TEST CASES GENERATED: [Total Count] test cases covering:
   - Functional: [count] test cases
   - Regression: [count] test cases
   - Smoke: [count] test cases
   - E2E: [count] test cases
   - Integration: [count] test cases
   - Negative: [count] test cases
   - Edge: [count] test cases

✅ REQUIREMENTS COVERAGE:
   - Total Requirements: [count]
   - Total Test Scenarios: [count]
   - Coverage: 100%

✅ FILE DETAILS:
   - Location: .github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases\
   - File Name: [ProjectName]_Zephyrimportready.csv
   - Format: Zephyr Scale Import-Ready CSV
   - Ready for Import: Yes ✅
```

**Example Response:**
```
# Spectrum Brand Manager - Zephyrimportready.csv created in .github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases

✅ TEMPLATE VALIDATION: PASSED
   - Template Source: ZephyrTestCaseTemplate.csv
   - Columns Validated: 16/16 columns match
   - Headers Match: 100% exact match
   - Format Compliance: ✅ Complete

✅ TEST CASES GENERATED: 65 test cases covering:
   - Functional: 25 test cases
   - Regression: 10 test cases
   - Smoke: 5 test cases
   - E2E: 8 test cases
   - Integration: 7 test cases
   - Negative: 6 test cases
   - Edge: 4 test cases

✅ REQUIREMENTS COVERAGE:
   - Total Requirements: 8
   - Total Test Scenarios: 45
   - Coverage: 100%

✅ FILE DETAILS:
   - Location: .github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases\
   - File Name: Spectrum_Brand_Manager_Zephyrimportready.csv
   - Format: Zephyr Scale Import-Ready CSV
   - Ready for Import: Yes ✅
```
  
---

### 6. Quality Checklist (MUST VERIFY BEFORE COMPLETING)

**🔴 PRE-SAVE VALIDATION - Complete ALL checks before calling create_file:**

**Template Compliance Checks:**
- [ ] ✅ Template file read from: `.github\agents\Test Case Generator\agents-context\skills\Test Case\Template\ZephyrTestCaseTemplate.csv`
- [ ] ✅ Template headers extracted and stored
- [ ] ✅ Generated CSV first line matches template headers exactly (character-by-character)
- [ ] ✅ No hardcoded headers used - all headers come from template file

**Column Structure Checks:**
- [ ] ✅ Generated CSV has exactly 16 columns
- [ ] ✅ Column order matches template exactly
- [ ] ✅ Column names match template exactly (case-sensitive, preserve hyphens/spaces)
- [ ] ✅ NO extra columns added (verify: no Priority, Status, Owner, Folder, Estimated Time, Test Script Type, Component, Precondition, Expected Result)
- [ ] ✅ NO columns removed or renamed from template
- [ ] ✅ All column headers from template are present

**Data Format Checks:**
- [ ] ✅ "Sub Domain" column is empty for ALL rows (main rows and step rows)
- [ ] ✅ Multi-step test cases: Step 2+ rows have ONLY "Test Step" populated, all other columns blank
- [ ] ✅ "Labels" column contains comma-separated values in ONE cell with quotes (e.g., `"Functional,Regression,Smoke"`)
- [ ] ✅ **"Requirement ID" column (column 16) contains BOTH REQ-XXX and TS-YYY in ONE cell with quotes**
- [ ] ✅ **CRITICAL: Format is `"REQ-001,TS-001"` with quotes - NOT `REQ-001,TS-001` without quotes**
- [ ] ✅ **CRITICAL: Each row has EXACTLY 16 columns - no 17th column (verify no TS-YYY split)**
- [ ] ✅ **The comma between REQ-XXX and TS-YYY is INSIDE the quotes**
- [ ] ✅ **Verify when writing CSV: Use format `...,"REQ-001,TS-001"` NOT `...,REQ-001,TS-001`**
- [ ] ✅ All test case rows have exactly 16 column values (blank columns counted as empty cells)

**🚨 MOST COMMON ERROR - REQUIREMENT ID COLUMN:**
- [ ] ✅ **Check EVERY test case row: Requirement ID must be `"REQ-XXX,TS-YYY"` in quotes**
- [ ] ✅ **The most frequent bug: Writing `REQ-001,TS-001` without quotes creates column 17**
- [ ] ✅ **Solution: ALWAYS wrap in quotes when generating CSV content**

**File Location Check:**
- [ ] ✅ File saved to: `.github\agents\Test Case Generator\agents-context\ZephyrReadyTestCases\`
- [ ] ✅ File name format: `ProjectName_Zephyrimportready.csv`

**Content Coverage Checks:**
- [ ] ✅ All 7 test types generated (Functional, Regression, Smoke, E2E, Integration, Negative, Edge)
- [ ] ✅ All requirements from RTM covered
- [ ] ✅ Each test scenario from RTM has corresponding test case(s)

**🔴 CRITICAL CSV STRUCTURE VALIDATION:**
- [ ] ✅ **Open generated CSV file and verify column count = 16 (NOT 17)**
- [ ] ✅ **Verify Requirement ID column (last column) shows values like: `"REQ-001,TS-001"` (both in quotes, single cell)**
- [ ] ✅ **Check no extra column appears after Requirement ID column**
- [ ] ✅ **All commas within cells are properly quoted to prevent column splitting**

**❌ IF ANY CHECK FAILS:**
```
DO NOT SAVE THE FILE
Report the specific failure(s)
Fix the issue(s)
Re-run validation checklist
Only proceed when ALL checks pass
```

**✅ AFTER ALL CHECKS PASS:**
- Create the CSV file using create_file tool
- Confirm file creation
- Report test case generation summary with validation status
