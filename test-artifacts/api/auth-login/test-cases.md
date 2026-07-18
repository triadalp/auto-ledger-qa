# Test Cases

| ID | Test Case | Expected Result | Status |
|----|-----------|-----------------|--------|
| LOGIN-01 | Successful login | 200, access token, refresh cookie | PASS |
| LOGIN-02 | Email normalization | Email trimmed and lowercased | PASS |
| LOGIN-03 | Incorrect password | 401 INVALID_CREDENTIALS | PASS |
| LOGIN-04 | Unknown email | 401 INVALID_CREDENTIALS | PASS |
| LOGIN-05 | Invalid request fields | 400 VALIDATION_ERROR | PASS |
| LOGIN-06 | Malformed JSON | 400 INVALID_JSON, API remains running | PASS |
| LOGIN-07 | Repeated successful login | Both requests succeed, refresh cookie updated | PASS |