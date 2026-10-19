# Auth Logout — Test Cases

## LOGOUT-01 — Successful Logout

**Priority:** High
**Status:** PASS

### Preconditions

* API server is running at `http://localhost:3000`.
* Test user is registered and logged in.
* A valid refresh token is stored in the `refreshToken` cookie.
* An active session exists in MongoDB.

### Test Steps

1. Open Postman.
2. Select `POST /api/auth/logout`.
3. Verify that a valid `refreshToken` cookie is sent with the request.
4. Send the request.
5. Check the response status and body.
6. Check the `Set-Cookie` response header.
7. Open MongoDB Compass and find the corresponding session.

### Expected Result

* HTTP status is `204 No Content`.
* Response body is empty.
* The server sends a `Set-Cookie` header to clear the refresh token.
* The session's `revokedAt` field changes from `null` to a date.
* The session's `updatedAt` field is updated.

### Actual Result

* HTTP `204 No Content` received.
* Response body was empty.
* `Set-Cookie` header instructed the client to clear the refresh token.
* Session revocation was confirmed in MongoDB.
* `revokedAt` and `updatedAt` were updated.

**Result: PASS**


## LOGOUT-02 — Refresh After Logout

**Priority:** High
**Status:** PASS

### Preconditions

* User is registered and logged in.
* A valid refresh token R1 has been saved.
* Logout has been successfully performed using R1.
* The corresponding session has `revokedAt` set to a date in MongoDB.

### Test Steps

1. Open Postman.
2. Restore the previously saved refresh token R1 in the `refreshToken` cookie.
3. Send `POST /api/auth/refresh`.
4. Check the response status and body.
5. Check the `Set-Cookie` response header.
6. Verify the session state in MongoDB Compass.

### Expected Result

* HTTP status is `401 Unauthorized`.
* Response contains error code `INVALID_REFRESH_TOKEN`.
* No new access token is issued.
* No new refresh token is issued.
* The revoked session remains unchanged in MongoDB.

### Actual Result

* HTTP `401 Unauthorized` received.
* Error code `INVALID_REFRESH_TOKEN` returned.
* No new access token or refresh token was issued.
* The revoked session remained unchanged.

**Result: PASS**


## LOGOUT-03 — Repeated Logout

**Priority:** Medium
**Status:** PASS

### Preconditions

* User has successfully logged in.
* Refresh token R1 has been saved.
* Logout has already been performed using R1.
* The corresponding session is revoked in MongoDB.

### Test Steps

1. Open Postman.
2. Set the `refreshToken` cookie to the previously saved token R1.
3. Send `POST /api/auth/logout` again.
4. Check the response status and body.
5. Check the corresponding session in MongoDB Compass.

### Expected Result

* HTTP status is `204 No Content`.
* Response body is empty.
* Repeated logout does not produce an error.
* The session remains revoked.
* Session data remains unchanged.

### Actual Result

* HTTP `204 No Content` received.
* Response body was empty.
* Repeated logout was handled successfully.
* Session data remained unchanged in MongoDB.

**Result: PASS**


## LOGOUT-04 — Logout Without Token

**Priority:** Medium
**Status:** PASS

### Preconditions

* API server is running.
* Postman is configured to send requests to `http://localhost:3000`.
* No `refreshToken` cookie is sent with the request.
* Existing sessions are available in MongoDB for comparison.

### Test Steps

1. Open Postman.
2. Remove the `refreshToken` cookie.
3. Select `POST /api/auth/logout`.
4. Verify in Postman Console that the request does not contain a `Cookie` header.
5. Send the request.
6. Check the response status and body.
7. Check the existing sessions in MongoDB Compass.

### Expected Result

* HTTP status is `204 No Content`.
* Response body is empty.
* Logout succeeds even without a refresh token.
* Existing sessions remain unchanged.

### Actual Result

* HTTP `204 No Content` received.
* Response body was empty.
* Postman Console confirmed that no cookie was sent.
* Existing sessions remained unchanged in MongoDB.

**Result: PASS**


## LOGOUT-05 — Unknown Refresh Token

**Priority:** Medium
**Status:** PASS

### Preconditions

* API server is running.
* An unknown test refresh token is prepared.
* Existing sessions are available in MongoDB for comparison.

### Test Steps

1. Open Postman.
2. Remove the current `refreshToken` cookie.
3. Create a new `refreshToken` cookie with an unknown test value.
4. Set the cookie path to `/api/auth`.
5. Send `POST /api/auth/logout`.
6. Check the response status and body.
7. Check the `Set-Cookie` response header.
8. Verify existing sessions in MongoDB Compass.

### Expected Result

* HTTP status is `204 No Content`.
* Response body is empty.
* The server sends a `Set-Cookie` header to clear the refresh token.
* No existing sessions are modified.

### Actual Result

* HTTP `204 No Content` received.
* Response body was empty.
* The server instructed the client to clear the refresh token.
* Existing sessions remained unchanged in MongoDB.

**Result: PASS**


## LOGOUT-06 — Independent User Sessions

**Priority:** High
**Status:** PASS

### Preconditions

* API server is running at `http://localhost:3000`.
* A registered test user exists.
* Postman and MongoDB Compass are available.

### Test Steps

1. Log in using `POST /api/auth/login`.
2. Save the issued refresh token as Token A.
3. Log in again using the same user credentials.
4. Save the second refresh token as Token B.
5. Open MongoDB Compass and verify that two separate active sessions exist.
6. Send `POST /api/auth/logout` using Token B.
7. Check the response status, body and `Set-Cookie` header.
8. Verify that only session B was revoked in MongoDB.
9. Replace the `refreshToken` cookie with Token A.
10. Send `POST /api/auth/refresh`.
11. Check the response status, body and new refresh token cookie.
12. Verify session changes in MongoDB.

### Expected Result

* Two independent sessions are created for the same user.
* Both sessions initially have `revokedAt: null`.
* Logout with Token B returns `204 No Content` and clears the refresh token cookie.
* Only session B is revoked.
* Session A remains active.
* Refresh with Token A returns `200 OK` and a new `accessToken`.
* A new refresh token is issued for session A.
* Session A's `refreshTokenHash` and `updatedAt` are updated.
* Session B remains unchanged after refreshing session A.
* No additional session is created during token rotation.

### Actual Result

* Two separate active sessions were created.
* Logout with Token B returned `204 No Content`.
* Session B was revoked while session A remained active.
* Refresh with Token A returned `200 OK`.
* New access and refresh tokens were issued.
* Token rotation was confirmed in MongoDB.
* Session B remained unchanged.
* No additional session was created.

**Result: PASS**
