# Registration API Requirements

## Feature

User registration API

## Endpoint

POST /api/auth/register

## Test Environment

- Branch: feat/auth-registration
- Commit: 88b510d
- API: Local
- Tool: Postman
- Node.js: v22.14.0

## Functional Requirements

- User can register with valid data.
- Email must be unique.
- All fields are required.
- Email must be normalized (trimmed and converted to lowercase).
- First name and last name must be trimmed.
- Password must:
  - contain 6-20 characters;
  - include at least one letter;
  - include at least one digit;
  - not contain whitespace.
- Invalid JSON must return a controlled validation error.
- API responses must never expose password or passwordHash.