
# Copilot Prompts Reference

## Convert Word to Markdown (M365 Copilot)
```
Convert this Word document into a markdown (.md) file and provide a download link.
```

## Excel Test Case Generation
```
Using Spectrum_Brand_Manager.md, generate Excel-ready test cases with columns:
Test Case ID, Test Case Name, Precondition, Test Steps, Expected Result, Component Name.
```

## Zephyr Template Generation
```
Generate test cases using the Zephyr template ZephyrScale.csv.
```

## Zephyr Step Correction Prompt
```
Each test case must start on a single row with all test metadata populated:
Name, Objective, Pre-condition, Test Step (Step 1), Test Data, Test Result, Labels, Technology Domain, Components, QA engineer, Fix versions, Affect versions, Automated, API, Jira, SubDomain.

If a test case has more than one step:
Step 1 must appear in the main test case row under the "Test Step" column
Step 2, Step 3, and subsequent steps must each appear on their own new rows beneath Step 1 under the "Test Step" column

For Step 2+ rows:
Only the "Test Step" column should contain text.
All other columns must be left blank.

Do NOT merge steps into a single row.
Do NOT place steps in the "Test Data" column.
Preserve step numbering exactly as:
Step 1:
Step 2:
Step 3:

Generate a Zephyr ready import csv file.
```

## Automation Prompt (VS Code Copilot)
```
Read the CSV file and automate these test cases.
```
