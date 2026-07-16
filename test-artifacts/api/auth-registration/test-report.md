# Registration API Test Report

## Project

Auto Ledger

## Feature

User Registration API

## Test Environment

- Branch: `feat/auth-registration`
- Commit: `88b510d`
- OS: Windows
- Node.js: `v22.14.0`
- API: Local
- Tool: Postman

## Test Scope

The following functionality was tested:

- Successful user registration
- Duplicate email validation
- Required fields validation
- Email normalization
- Name normalization
- Password validation
- Malformed JSON handling

## Test Results

| Result | Count |
|---------|------:|
| Total test cases | 7 |
| Passed | 6 |
| Failed | 1 |
| Blocked | 0 |

## Defects Found

| ID | Title | Severity | Status |
|----|-------|----------|--------|
| BUG-API-001 | Registration rejects uppercase email instead of normalizing it | Medium | Open |

## Conclusion

The Registration API successfully passed all functional and validation scenarios except email normalization.

The endpoint correctly validates required fields, password rules, duplicate email detection, malformed JSON handling, and trims first and last names.

One defect was identified: emails containing uppercase characters are rejected instead of being normalized to lowercase as specified in the requirements.