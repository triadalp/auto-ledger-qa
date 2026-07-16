# Registration API Test Cases

| ID | Test Case | Expected Result | Status |
|----|-----------|-----------------|--------|
| REG-01 | Register user with valid data | User is created successfully. Status 201. Response contains user.id, firstName, lastName and email. Password is not returned. | PASS |
| REG-02 | Register user with an existing email | Status 409. Error code: EMAIL_ALREADY_EXISTS. | PASS |
| REG-03 | Submit empty required fields | Status 400. Validation errors are returned for all required fields. | PASS |
| REG-04 | Register using uppercase email with surrounding spaces | Status 201. Email is trimmed and converted to lowercase. | **FAIL** |
| REG-05 | Register using first and last names with surrounding spaces | Status 201. Names are trimmed before saving. | PASS |
| REG-06 | Validate password rules | Status 400 for invalid passwords. Password is never returned in response. | PASS |
| REG-07 | Send malformed JSON | Status 400. Error code: INVALID_JSON. API remains available after request. | PASS |