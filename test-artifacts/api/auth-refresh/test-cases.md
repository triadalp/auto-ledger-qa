# Auth Refresh — Test Cases

## REFRESH-01 — Successful Token Refresh

**Priority:** High
**Status:** PASS

### Preconditions

* API server is running at `http://localhost:3000`.
* Test user is registered.
* User has successfully logged in.
* A valid refresh token is stored in the `refreshToken` cookie.
* An active session exists in MongoDB.

### Test Steps

1. Open Postman.
2. Select `POST /api/auth/refresh`.
3. Verify that the valid `refreshToken` cookie is present.
4. Send the request.
5. Check the response status and body.
6. Check the `Set-Cookie` response header.
7. Open MongoDB Compass and inspect the corresponding session.

### Expected Result

* HTTP status is `200 OK`.
* Response contains a new `accessToken`.
* A new refresh token is issued in the cookie.
* The previous refresh token becomes invalid.
* The session's `refreshTokenHash` is updated in MongoDB.
* The session remains active (`revokedAt: null`).

### Actual Result

* HTTP `200 OK` received.
* New access token and refresh token were issued.
* Refresh token rotation was confirmed.
* Session hash was updated in MongoDB.
* Session remained active.

**Result: PASS**


## REFRESH-02 — Reuse of Old Refresh Token

**Priority:** High
**Status:** PASS

### Preconditions

* User is registered and logged in.
* An active session exists in MongoDB.
* Refresh token R1 has been saved.
* Token R1 has already been used to obtain a new token R2.

### Test Steps

1. Open Postman.
2. Replace the current `refreshToken` cookie with the old token R1.
3. Send `POST /api/auth/refresh`.
4. Check the response status and body.
5. Check the session in MongoDB Compass.

### Expected Result

* HTTP status is `401 Unauthorized`.
* Response contains error code `INVALID_REFRESH_TOKEN`.
* The old token R1 cannot be reused.
* No new refresh token is issued.
* The session remains unchanged.

### Actual Result

* HTTP `401 Unauthorized` received.
* Error code `INVALID_REFRESH_TOKEN` returned.
* Old token R1 was rejected.
* No new refresh token was issued.
* Session data remained unchanged.

**Result: PASS**


## REFRESH-03 — Refresh Without Token

**Priority:** High
**Status:** PASS

### Preconditions

* API server is running.
* Postman is configured to send requests to `http://localhost:3000`.
* No `refreshToken` cookie is present in the request.

### Test Steps

1. Open Postman.
2. Remove the `refreshToken` cookie.
3. Select `POST /api/auth/refresh`.
4. Send the request.
5. Check the response status and body.

### Expected Result

* HTTP status is `401 Unauthorized`.
* Response contains error code `INVALID_REFRESH_TOKEN`.
* No new access token is issued.
* No new refresh token is issued.

### Actual Result

* HTTP `401 Unauthorized` received.
* Error code `INVALID_REFRESH_TOKEN` returned.
* No new access token or refresh token was issued.

**Result: PASS**


## REFRESH-04 — Unknown Refresh Token

**Priority:** High
**Status:** PASS

### Preconditions

* API server is running.
* A test refresh token that does not belong to any existing session is prepared.
* Postman is configured to send the token in the `refreshToken` cookie.

### Test Steps

1. Open Postman.
2. Remove the current `refreshToken` cookie.
3. Create a new `refreshToken` cookie with an unknown test value.
4. Set the cookie path to `/api/auth`.
5. Send `POST /api/auth/refresh`.
6. Check the response status and body.
7. Check that no new refresh token was issued.

### Expected Result

* HTTP status is `401 Unauthorized`.
* Response contains error code `INVALID_REFRESH_TOKEN`.
* No new access token is issued.
* No new refresh token is issued.
* Existing sessions remain unchanged.

### Actual Result

* HTTP `401 Unauthorized` received.
* Error code `INVALID_REFRESH_TOKEN` returned.
* No new access token or refresh token was issued.
* Existing sessions remained unchanged.

**Result: PASS**


## REFRESH-05 — Expired Session

**Priority:** High
**Status:** PASS

### Preconditions

* API server is running.
* User is registered and logged in.
* A valid refresh token is stored in the `refreshToken` cookie.
* The corresponding session exists in MongoDB.

### Test Steps

1. Open MongoDB Compass.
2. Find the session corresponding to the current refresh token.
3. Change the `expiresAt` field to a date in the past.
4. Save the changes.
5. Open Postman.
6. Send `POST /api/auth/refresh` with the original refresh token.
7. Check the response status and body.
8. Check the session in MongoDB.

### Expected Result

* HTTP status is `401 Unauthorized`.
* Response contains error code `INVALID_REFRESH_TOKEN`.
* The expired session cannot be refreshed.
* No new access token is issued.
* No new refresh token is issued.

### Actual Result

* HTTP `401 Unauthorized` received.
* Error code `INVALID_REFRESH_TOKEN` returned.
* Expired session was rejected.
* No new access token or refresh token was issued.

**Result: PASS**


## REFRESH-06 — Revoked Session

**Priority:** High
**Status:** PASS

### Preconditions

* API server is running.
* User is registered and logged in.
* A valid refresh token is saved.
* The corresponding session exists in MongoDB.

### Test Steps

1. Open MongoDB Compass.
2. Find the session corresponding to the saved refresh token.
3. Change `revokedAt` from `null` to the current date and time.
4. Save the changes.
5. Open Postman.
6. Send `POST /api/auth/refresh` using the saved refresh token.
7. Check the response status and body.
8. Verify that no new tokens were issued.

### Expected Result

* HTTP status is `401 Unauthorized`.
* Response contains error code `INVALID_REFRESH_TOKEN`.
* The revoked session cannot be refreshed.
* No new access token is issued.
* No new refresh token is issued.

### Actual Result

* HTTP `401 Unauthorized` received.
* Error code `INVALID_REFRESH_TOKEN` returned.
* Revoked session was rejected.
* No new access token or refresh token was issued.

**Result: PASS**
