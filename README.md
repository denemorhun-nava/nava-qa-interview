# Login Page — QA Interview Exercise

## Context

You are testing [the login page](https://denemorhun-nava.github.io/nava-qa-interview/) for an application.

- Login validates the user account through the backend.
- Users must log in before accessing the dashboard or continuing their main workflow.
- Users may have different roles and account states.

---

## Requirements

### Username
- Required field
- 30 character limit
- Does not allow spaces

### Password
- Required field
- Masked
- 10 character limit
- Only allows alpha characters and these special characters: `!@#$%`
- typing in *secret* will unlock the dashboard

### Page-level validations
- Validations are performed when **Sign in** is clicked
- Validation messages appear under the field they apply to
- Validation messages:
  - `"This field is required"`
  - `"Invalid username/password"`

---

## User Interface

Open [the login page](https://denemorhun-nava.github.io/nava-qa-interview/) in your browser to interact with the login page.

### Partial HTML

```html
<body>
  <div class="login-container" data-testid="login-wrapper">
    <h2 id="login-title">Login</h2>
    <form action="#" method="POST" aria-labelledby="login-title" data-testid="login-form">
      <div class="form-group">
        <label id="username-label" for="username">Username</label>
        <input type="text" id="username" name="username"
          aria-labelledby="username-label" data-testid="username-field" required>
      </div>
      <div class="form-group">
        <label id="password-label" for="password">Password</label>
        <input type="password" id="password" name="password"
          aria-labelledby="password-label" data-testid="password-field" required>
      </div>
      <div class="form-group">
        <button type="submit" data-testid="login-submit-button">Sign In</button>
      </div>
    </form>
  </div>
</body>
```

## Screenshot

![Login page](UI.png)

---

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



