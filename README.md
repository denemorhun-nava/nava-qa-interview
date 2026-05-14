# Login Page — QA Interview Exercise

## Context

You are testing the Login Flow for a [NAVA application](https://denemorhun-nava.github.io/nava-qa-interview/).

- Login is handled through a mocked backend API and mocked user data store.
- The login page has frontend field validations for username and password.
- After the user clicks Sign-in, the mocked backend determines whether the user is allowed to log in.
- Users may have different account states, such as active, locked, or disabled.
- Users may have different roles, such as admin or standard user.
- Users must log in before accessing the dashboard or continuing their main workflow.

Your goal is to design a test strategy for the login flow, not just test the login form. 

Include field validation, authentication behavior, user account states, role/access differences, token login, error handling, and any missing requirements you would clarify before testing.

---

## Requirements

### Username
- Required field
- 5 character lower limit
- 20 character upper limit
- Does not allow spaces
- only alpha characters and @ and .

### Password
- Required field
- Masked
- 5 character lower limit
- 10 character limit
- Only allows alpha characters and these special characters: `!@#$%`

### Sign-in Button
  - Clickable

### Page-level validations
- Validations are performed when **Sign in** is clicked
- Validation messages appear under the field they apply to
- Validation messages:
  - `"This field is required"`
  - `"Invalid username/password"`

### Dashboard
- Entering *secret!* in password field will enable user to authenticate
- Dashboard is standard user view for this exercise

---

### Backend / Account Behavior

The backend may return different outcomes depending on the user account.

Candidates should consider scenarios such as:

- Valid active user
- Invalid username
- Invalid password
- Locked account
- Disabled account
- Pending or unverified account
- Expired account
- Different user roles or account types
- User authenticated successfully but not authorized for the dashboard
- Token-based login
- Expired or invalid token

## Screenshot

![Login page](UI.png)

---

### Partial HTML

```html
<body>
  <div class="login-container" data-testid="login-wrapper">
    <h2 id="login-title">Login</h2>
    <form aria-labelledby="login-title" data-testid="login-form" novalidate>
      <label for="username">Username</label>
      <input type="text" id="username" name="username"
        aria-labelledby="login-title" data-testid="username-field">
      <label for="password">Password</label>
      <input type="password" id="password" name="password"
        aria-labelledby="login-title" data-testid="password-field">
      <button type="submit" data-testid="login-submit-button">Sign In</button>
    </form>
  </div>
</body>
```

## API

| Method | Endpoint | Notes |
|--------|----------|-------|
| GET | `/v1/user/login?username=<username>&password=<password>` | Password-based login |
| GET | `/v1/user/login?token=<token>` | Token-based login |
| POST | `/v1/user/account/create` | Body: `{ username, password, email }` |
| POST | `/v1/user/account/account_email` | Body: `{ username, type }` |

`email_type` accepts: `"forgot_password"` or `"forgot_username"`

---

## Database Schema

```sql
TABLE Users (
    user_id           INT PRIMARY KEY AUTO_INCREMENT,
    username          VARCHAR(50) UNIQUE NOT NULL,
    email             VARCHAR(100) UNIQUE NOT NULL,
    password_hash     VARCHAR(255) NOT NULL,
    registration_date DATETIME DEFAULT CURRENT_TIMESTAMP
) 
```

## User Interface

Open [the login page](https://denemorhun-nava.github.io/nava-qa-interview/) in your browser to interact with the login page.



