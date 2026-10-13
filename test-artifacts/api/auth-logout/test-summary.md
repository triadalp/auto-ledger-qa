# Auth Logout — Test Summary

## Test Information

* **Project:** Auto Ledger
* **Module:** API Authentication — Logout
* **Environment:** Local Development
* **API:** http://localhost:3000
* **Tools:** Postman, MongoDB Compass
* **Database:** MongoDB (autoLedgerDB)
* **Branch:** feat/auth-logout
* **Commit:** 102e587

## Test Scope

The following scenarios were tested:

* LOGOUT-01 — Successful logout with a valid refresh token.
* LOGOUT-02 — Refresh attempt after logout.
* LOGOUT-03 — Repeated logout with a revoked token.
* LOGOUT-04 — Logout without a refresh token.
* LOGOUT-05 — Logout with an unknown refresh token.
* LOGOUT-06 — Logout with two independent user sessions.

## Test Results

| Status  | Count |
| ------- | ----: |
| Passed  |     6 |
| Failed  |     0 |
| Blocked |     0 |
| Total   |     6 |

## Verification

* API response status codes and response bodies were checked in Postman.
* Refresh token cookie clearing was verified through response headers.
* Session revocation was verified in MongoDB Compass.
* Repeated logout requests were handled successfully.
* Logout with missing and unknown tokens was verified.
* Session isolation was confirmed: logging out of session B did not affect session A.
* Refresh token rotation continued to work for the active session A.

## Conclusion

**QA Status: PASSED**

All 6 test scenarios passed.

No defects were found during the executed tests.
