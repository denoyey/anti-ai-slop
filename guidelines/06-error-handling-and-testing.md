# 06. Error Handling, Logging, and Verification Standard

[English](06-error-handling-and-testing.md) | [Bahasa Indonesia](id/06-error-handling-and-testing.md)

---

This document establishes engineering standards to ensure AI-generated code eliminates silent failures, handles errors consistently, and provides empirical verification.

---

## 1. Error Handling Rules (Zero Silent Failures)

❌ **STRICTLY FORBIDDEN:**
```typescript
// FORBIDDEN: Silently swallowing exceptions
try {
  await processPayment();
} catch (error) {
  // empty / silent pass
}
```

### Core Principles:
1. **Custom Domain Exceptions:**
   - Use semantic custom exception classes with clear error codes and mapped HTTP status codes (e.g., `EntityNotFoundException`, `UnauthorizedException`, `ValidationException`).
2. **Centralized Error Middleware:**
   - Unhandled exceptions must be caught by a centralized error middleware at the outer layer of the application.
   - In production, 500 error responses must remain sanitized: `{"status": "error", "message": "An unexpected error occurred"}`, never leaking raw database queries or traces.
3. **Explicit Error Boundaries (Frontend):**
   - Place Error Boundaries at route and widget boundaries so a failure in one component does not crash the entire application.

---

## 2. Structured Logging & Observability

1. **Structured Logging:**
   - Format logs as structured JSON (`timestamp`, `level`, `context`, `traceId`, `message`).
2. **PII Masking & Redaction:**
   - ❌ **Forbidden:** Never write passwords, bearer tokens, credit card numbers, or sensitive credentials to log streams.
   - Always sanitize request payloads before passing them to the logger:
     ```typescript
     logger.info('User login attempt', { email: sanitizeEmail(user.email) });
     ```

---

## 3. Testing & Verification Standards

Every new feature or bugfix must have associated test scenarios:

1. **Unit Testing:**
   - Test pure business logic in isolation without hitting live databases (use mocks or test doubles).
   - Test both the happy path AND edge cases (boundary limits, invalid schemas).
2. **Integration Testing:**
   - Test database queries and external adapters against containerized or test database instances.
3. **Security Testing:**
   - Test authentication bypass attempts, SQL injection payloads, XSS vectors, and unauthorized resource access (IDOR).
4. **Empirical Verification Before Declaring Success:**
   - AI assistants must run the relevant test runner (`npm test`, `pytest`, `cargo test`, `go test`) or linter/typecheck before claiming that a fix or feature is complete.
   - Never assert that code "works perfectly" without empirical execution proof.
