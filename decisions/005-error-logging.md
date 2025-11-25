# Error Logging

Not every error should be logged. The goal is to log what helps with debugging and traceability, and avoid logging noise that makes real issues harder to find.

## Errors that should be logged

### 1. Unexpected errors

- Errors that are not defined Domain/Application/Infrastructure errors.

### 2. Infrastructure errors

- Database failures.
- Network timeouts.
- External service issues (API calls, email-service, storage-service etc).
- Configuration or connection failures.

### 3. Application errors that indicate workflow failure

- When a use-case fails due to an unexpected condition.
- When the application layer wraps another error for added context.

```
e.g.
A "CreateOrder" use-case fails because the payment service is down (infrastructure error).
The application layer catches the infrastructure error, wraps it into a "ApplicationError" application error, and throws it up.
This "ApplicationError" should be logged.

```

### 4. Errors reaching the API boundary

- Any error that bubbles up to the API layer and results in a 5xx response.

---

## Errors that should not be logged

### 1. Expected domain rule failures

Business rule violations like invalid dates or forbidden entity states, because these are normal control-flow, not system-level problems.

### 2. Validation errors

Invalid user input, missing fields, wrong format. These should be surfaced to the user, not logged.

### 3. Authorization denials

Cases where a user simply lacks permission is also not a system failure, no need for logs.

### 4. Re-thrown or already logged errors

Errors must be logged once, usually in the API layer.

---
