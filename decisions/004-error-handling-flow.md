# Error Handling and Error Management

Error handling in this starter should be simple, predictable, and aligned with the layered structure. Errors should move upward through the system in a controlled way, eventually becoming clear messages for end users and useful traces for debugging.

## How errors surface, bubble, and are handled across layers

Each layer handles errors differently, but they all follow a consistent flow:  
**Domain → Application → API → End User / Logs**

### Domain Layer

- Throws domain-specific errors when business rules or invariants fail.
- Does not catch errors from deeper layers (because there are none).
- Never exposes technical details—only meaningful rule violations.
- Errors here represent pure business failures.

**Error flow:**  
Domain errors bubble up to the Application layer unchanged.

---

### Application Layer

- Calls domain logic and catches domain errors when needed.
- Wraps errors only when additional context is required (e.g., which use-case failed).
- Throws application-level errors when an action cannot complete.
- Avoids UI or transport-related details.

**Error flow:**  
Application errors (or wrapped domain errors) bubble up to the API layer.

---

### Infrastructure Layer

- Throws errors related to external systems (DB, network, storage, APIs).
- These errors contain technical details useful for debugging.
- They should never leak raw external error shapes into other layers.
- If needed, infrastructure errors may be wrapped into higher-level errors before leaving this layer.

**Error flow:**  
Infrastructure errors bubble up through the Application layer, which may wrap them or pass them through.

---

### API Layer

- Receives domain/application/infrastructure errors.
- Translates them into clean, user-facing responses with no internal details.
- Never exposes stack traces or system internals.
- Uses a consistent error shape across all endpoints or delivery mechanisms.

**Error flow:**  
This layer produces:

- A safe output for the end user
- A detailed log entry for debugging

---

## What end users should see

- A short, readable message
- A consistent and predictable error structure
- No stack traces
- No identifiers that reveal sensitive internals

---

## What developers should see (via logs)

- The original error (domain/application/infrastructure)
- Stack traces
- Metadata about where the error occurred
- Request or correlation id when available

---
