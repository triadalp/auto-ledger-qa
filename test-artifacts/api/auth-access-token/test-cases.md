# Test Cases: Access Token Authentication

**Project:** Auto Ledger
**Module:** API Authentication
**Endpoint:** `GET /api/auth/me`
**Environment:** Local API, Postman

## AUTH-01: Valid Access Token

**Steps:**

1. Log in using `POST /api/auth/login`.
2. Copy the access token.
3. Send `GET /api/auth/me` with a valid Bearer token.

**Expected Result:**

* HTTP 200 OK.
* Response contains `user.id`, `user.firstName`, `user.lastName`, `user.email`.
* `passwordHash` is not returned.
* User data matches the logged-in account.

**Actual Result:** As expected.
**Status:** PASS

## AUTH-02: Missing Access Token

**Steps:**

1. Open `GET /api/auth/me`.
2. Remove the Authorization header.
3. Send the request.

**Expected Result:**

* HTTP 401 Unauthorized.
* Error code: `UNAUTHORIZED`.
* Error message: `Authentication required`.

**Actual Result:** As expected.
**Status:** PASS

## AUTH-03: Malformed Authorization Header

**Steps:**

1. Send a request with `Authorization: Basic <accessToken>`.
2. Send a request with `Authorization: Bearer` (without a token).
3. Send a request with `Authorization: Bearer <accessToken> extra`.

**Expected Result for Each Request:**

* HTTP 401 Unauthorized.
* Error code: `UNAUTHORIZED`.
* No user data returned.

**Actual Result:** All three requests were rejected as expected.
**Status:** PASS

## AUTH-04: Invalid Access Token

**Steps:**

1. Log in and obtain a valid access token.
2. Change one character in the token.
3. Send `GET /api/auth/me` with the modified token.

**Expected Result:**

* HTTP 401 Unauthorized.
* Error code: `UNAUTHORIZED`.
* Error message: `Authentication required`.
* No user data or technical JWT errors returned.

**Actual Result:** As expected.
**Status:** PASS

## AUTH-05: Expired Access Token

**Steps:**

1. Set `ACCESS_TOKEN_TTL_SECONDS=15` in `apps/api/.env`.
2. Restart the API.
3. Log in and obtain a new access token.
4. Wait 20–30 seconds.
5. Send `GET /api/auth/me` with the expired token.
6. Restore `ACCESS_TOKEN_TTL_SECONDS=900` and restart the API.

**Expected Result:**

* HTTP 401 Unauthorized.
* Error code: `UNAUTHORIZED`.
* Error message: `Authentication required`.
* No user data returned.

**Actual Result:** As expected. Configuration restored.
**Status:** PASS
