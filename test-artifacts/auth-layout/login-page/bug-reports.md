# Login Page Bug Reports

## BUG-001: Login form accepts spaces-only password

Status: Fixed  
Retest result: PASS

### Branch

`feat/auth-layout`

### Page

`/login`

### Actual result

The login form was submitted when the Password field contained only spaces.  
The submitted data was visible in DevTools Console.

### Expected result

Password field with spaces only should be invalid.  
The form should not be submitted and a password validation error should be shown.

### Steps to reproduce

1. Open `/login`.
2. Enter a valid email.
3. Enter spaces only in the Password field.
4. Click the Sign in button.
5. Check DevTools Console.

### Severity

Medium

### Priority

Medium

### Retest

After the fix:

- empty password shows the required error;
- whitespace-only password shows a separate validation error;
- validation runs on submit;
- validation revalidates while correcting the field;
- form is not submitted with whitespace-only password.

### Retest result

PASS

### Screenshot

`screenshots/BUG-001-login-password-spaces-only.png`