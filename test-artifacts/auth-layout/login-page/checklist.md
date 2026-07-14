# Login Page Checklist

## Environment

- OS: Windows
- Browser: Chrome
- Project branch: `feat/auth-layout`
- Page: `/login`
- Run commands:
  - `npm install`
  - `npm run build`
  - `npm run preview`

## Login page layout

| ID | Check | Status | Comment |
|---|---|---|---|
| LOGIN-01 | Login page opens at `/login` | PASS | |
| LOGIN-02 | Login page opens without application sidebar | PASS | |
| LOGIN-03 | Login page opens without application header | PASS | |

## Login form elements

| ID | Check | Status | Comment |
|---|---|---|---|
| LOGIN-04 | Email field is displayed | PASS | |
| LOGIN-05 | Password field is displayed | PASS | |
| LOGIN-06 | Sign in button is displayed | PASS | |
| LOGIN-07 | Sign up link is displayed | PASS | |
| LOGIN-08 | Sign up link redirects to `/register` | PASS | |

## Required fields validation

| ID | Check | Status | Comment |
|---|---|---|---|
| LOGIN-09 | Empty form submit shows Email required error | PASS | |
| LOGIN-10 | Empty form submit shows Password required error | PASS | |
| LOGIN-11 | Empty form is not submitted | PASS | |

## Email validation

| ID | Check | Status | Comment |
|---|---|---|---|
| LOGIN-12 | Invalid email format, for example `test`, shows email format error | PASS | |
| LOGIN-13 | Form with invalid email is not submitted | PASS | |

## Password validation

| ID | Check | Status | Comment |
|---|---|---|---|
| LOGIN-14 | Valid email and regular non-empty password can be submitted | PASS | |
| LOGIN-15 | Submitted data is visible in browser console | PASS | Console shows submitted email and password object. |
| LOGIN-16 | Password field with spaces only is invalid | RETEST PASS | Initially failed. Fixed by developer and successfully retested. See BUG-001. |

## Build and preview

| ID | Check | Status | Comment |
|---|---|---|---|
| ENV-01 | `npm run build` passed | PASS | |
| ENV-02 | `npm run preview` launched successfully | PASS | |