# Register Page Requirements

## Page Information

**Branch:** feat/auth-layout

**Page:** /register

---

## Page Layout

- Register page opens without application sidebar or header.
- Registration form is displayed correctly.

---

## Form Fields

The registration form contains the following required fields:

- First name
- Last name
- Email
- Password
- Repeat password

---

## Navigation

- "Back" link redirects the user to the **/login** page.

---

## Form Validation

### First Name

- Required field.

### Last Name

- Required field.

### Email

- Required field.
- Must accept only a valid email format.

### Password

- Required field.
- Must contain at least 6 characters.
- Must contain at least one letter.
- Password consisting only of whitespace must be rejected.

### Repeat Password

- Required field.
- Must match the Password field.
- Must be revalidated after the Password field is changed.

---

## Form Submission

### Invalid Data

- Invalid form must not be submitted.
- Appropriate validation errors must be displayed.

### Valid Data

- Form is submitted successfully.
- Submitted data is visible in the browser console.

---

## Responsive Behavior

- On small viewport height, the register page can be scrolled.