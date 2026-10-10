# Login API — Regression Test Report

## General Information

* **Project:** Auto Ledger
* **Testing Type:** Manual Regression Testing
* **Test Date:** 2026-10-10
* **Environment:** Windows, Local API, Postman, MongoDB Compass
* **Branch:** `feat/auth-logout`
* **Commit:** `102e587`
* **API Endpoint:** `POST /api/auth/login`

## Objective

Verify that the Login API continues to work correctly after the implementation of the Logout functionality.

## Test Execution Results

| Test Case ID | Test Scenario                | Result |
| ------------ | ---------------------------- | ------ |
| LOGIN-01     | Successful login             | PASS   |
| LOGIN-02     | Email normalization          | PASS   |
| LOGIN-03     | Incorrect password           | PASS   |
| LOGIN-04     | Unknown email                | PASS   |
| LOGIN-05     | Invalid fields (3 scenarios) | PASS   |
| LOGIN-06     | Malformed JSON               | PASS   |
| LOGIN-07     | Repeated successful login    | PASS   |

## Additional Verification

* Verified successful authentication with valid credentials.
* Verified that invalid credentials return the expected error responses.
* Verified that invalid request data is rejected.
* Verified that malformed JSON does not cause the API to stop working.
* Verified refresh token cookie attributes: `HttpOnly`, `Path=/api/auth`, `SameSite=Lax`.
* Verified authentication session creation in MongoDB (`authSessions`).
* Verified that a new login replaces the existing refresh token cookie in Postman.
* Verified that sensitive authentication data is not exposed in the login response body.

## Test Summary

* **Total Test Cases:** 7
* **Passed:** 7
* **Failed:** 0
* **Blocked:** 0
* **Bugs Found:** 0

## Conclusion

**PASS**

All Login API regression test cases passed.

The Login API continues to work according to the documented requirements on branch `feat/auth-logout`.

No defects were identified during this testing cycle.

**Note:** This report covers Login API regression testing only. Refresh Token and Logout API testing will be documented separately.
