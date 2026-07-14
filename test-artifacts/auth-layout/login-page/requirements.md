# Login Page Requirements

## Branch

`feat/auth-layout`

## Page

`/login`

## Scope

Check the Login page layout and form validation.

## Expected behavior

- Login page opens without application sidebar/header.
- Email field is displayed.
- Password field is displayed.
- Sign in button is displayed.
- Sign up link is displayed.
- Sign up link redirects to `/register`.

## Validation

### Empty form

When submitting an empty form:

- Email required error should be shown.
- Password required error should be shown.
- Invalid form should not be submitted.

### Invalid email format

When entering an invalid email format, for example `test`:

- Email format error should be shown.
- Invalid form should not be submitted.

### Valid form

When entering a valid email and a regular non-empty password:

- Form should be submitted.
- Submitted data should be visible in browser console.

## Additional validation check

Password field should not accept whitespace-only value as a valid password.

## Expected result

- Invalid form is not submitted.
- Valid form is submitted.
- Submitted data is visible in browser console.