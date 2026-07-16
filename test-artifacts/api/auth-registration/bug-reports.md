# Bug Reports

---

## BUG-API-001

### Title

Registration API rejects uppercase email instead of normalizing it

### Status

Open

### Severity

Medium

### Priority

Medium

### Environment

- Branch: `feat/auth-registration`
- Commit: `88b510d`
- OS: Windows
- Node.js: `v22.14.0`
- Tool: Postman
- API: Local

### Preconditions

- Local API is running.
- A new unused email is available.

### Steps to Reproduce

1. Send a `POST /api/auth/register` request.
2. Enter valid registration data.
3. Use an email containing uppercase letters and surrounding spaces.
4. Send the request.

### Test Data

```json
{
  "firstName": "Borys",
  "lastName": "Presniak",
  "email": "  MARIA.TEST002@GMAIL.COM  ",
  "password": "<hidden>"
}
```

### Expected Result

- Status `201 Created`
- Email is trimmed.
- Email is converted to lowercase.
- User is created successfully.

### Actual Result

- Status `400 Bad Request`
- Error code: `VALIDATION_ERROR`
- Email field contains the error:

```text
Invalid lowercase
```

### Reproducibility

Always

### Attachments

- `screenshots/reg-04-fail.png`