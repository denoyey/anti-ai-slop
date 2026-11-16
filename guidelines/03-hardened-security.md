# 03. Hardened Security & Anti-Bypass Standard

[English](03-hardened-security.md) | [Bahasa Indonesia](id/03-hardened-security.md)

---

This document defines **non-negotiable security requirements**. AI coding assistants are strictly prohibited from generating code with security flaws, ranging from Low to Critical severity, spanning classical vulnerabilities (OWASP Top 10) to modern API and supply chain exploits.

---

## 1. Core Principles: Zero-Trust & Defense-in-Depth

1. **Never Trust User Input:**
   - Validate and sanitize all input on the server side, never relying on client-side validation alone.
   - Enforce type, format, length, range, and regex pattern constraints.
2. **Fail Securely:**
   - When authentication or validation fails, deny access by default (*deny by default*).
   - Never return internal stack traces, database error messages, or environment secrets in client responses.
3. **Principle of Least Privilege:**
   - Database roles, runtime containers, and API tokens must only possess the bare minimum permissions required.

---

## 2. Threat Mitigation Matrix (OWASP Top 10 & CWE)

### A. Injection Prevention (SQLi, NoSQLi, Command Injection)
- **SQL Injection:**
  - **MANDATORY:** Always use parameterized queries / prepared statements or safe ORM mappings.
  - ❌ **STRICTLY FORBIDDEN:** Concatenating raw strings into SQL queries:
    ```typescript
    // FORBIDDEN:
    db.query(`SELECT * FROM users WHERE email = '${email}'`);
    // MANDATORY:
    db.query('SELECT * FROM users WHERE email = $1', [email]);
    ```
- **Command Injection:**
  - Avoid shell execution functions (`exec`, `eval`, `system`, `subprocess.shell=True`).
  - If binary execution is unavoidable, pass argument arrays without shell interpolation and validate arguments against strict whitelists.

### B. Broken Object Level Authorization (BOLA / IDOR)
- **IDOR (Insecure Direct Object Reference):**
  - **MANDATORY:** Whenever modifying, querying, or deleting a resource by ID (e.g., `/api/orders/:id`), the backend **MUST** verify ownership against the authenticated user:
    ```typescript
    // FORBIDDEN: Only checking the route param
    const order = await orderRepo.findById(req.params.id);

    // MANDATORY: Scoped by the authenticated user ID
    const order = await orderRepo.findOne({
      where: { id: req.params.id, userId: req.user.id }
    });
    if (!order) throw new NotFoundOrForbiddenException();
    ```

### C. Broken Authentication & Session Security
- **Password Hashing:**
  - Use modern, memory-hard hashing algorithms: **Argon2id** (preferred) or **bcrypt** (work factor >= 12).
  - ❌ **Forbidden:** MD5, SHA1, plain SHA256 without salt/stretching.
- **JWT & Token Management:**
  - Keep Access Token expiration short (15–60 minutes).
  - Store Refresh Tokens in the database to support revocation and blocklisting.
  - Enforce explicit signing algorithms to prevent algorithm confusion attacks (e.g., switching RS256 to `none` or HS256).
- **Cookie Security:**
  - Session and auth cookies must always specify: `HttpOnly`, `Secure`, `SameSite=Strict` (or `Lax`), and appropriate `Domain` attributes.

### D. Cross-Site Scripting (XSS) & Content Injection
- **Output Encoding:**
  - Always HTML-escape dynamic data rendered in the browser.
  - ❌ **Forbidden:** Using `dangerouslySetInnerHTML`, `v-html`, or `innerHTML` unless input has been processed by a trusted sanitizer (e.g., `DOMPurify`).
- **Content Security Policy (CSP):**
  - Enforce strict CSP headers: disallow `unsafe-inline` and `unsafe-eval` where feasible.

### E. Mass Assignment & Parameter Tampering
- Never pass unvalidated request payloads directly to database entities:
  ```typescript
  // FORBIDDEN: Attackers can inject { "role": "admin", "balance": 999999 }
  await User.create(req.body);

  // MANDATORY: Use DTO / Schema Validators (Zod, Pydantic, class-validator)
  const validatedData = CreateUserSchema.parse(req.body);
  await User.create({
    name: validatedData.name,
    email: validatedData.email
  });
  ```

### F. Server-Side Request Forgery (SSRF)
- If the application makes outbound HTTP requests based on user input:
  - Enforce the `https://` protocol only.
  - Block internal / private IP ranges: `127.0.0.1`, `localhost`, `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, and cloud metadata endpoints (`169.254.169.254`).
  - Whitelist destination domains when possible.

### G. File Upload & Media Security
- Never rely solely on client-provided file extensions or `Content-Type` headers.
- Verify file types using **magic bytes (file signatures)**.
- Rename files using cryptographically secure UUIDs (do not keep original filenames).
- Store files outside public web roots or in Object Storage (S3 / GCS) with private ACLs or time-limited presigned URLs.
- Enforce strict maximum payload size limits.

### H. Rate Limiting & DoS Mitigation
- Apply rate limiters to all sensitive endpoints:
  - Login (prevent brute-force credential stuffing)
  - Registration (prevent bot account spam)
  - Password reset and OTP verification (prevent OTP enumeration)
- Limit HTTP body parser sizes (e.g., maximum 1MB for JSON payloads) to mitigate payload-based Denial of Service.

---

## 3. Secrets Management

- ❌ **ZERO TOLERANCE: Never commit API keys, database credentials, JWT secrets, or private keys to git.**
- Always provide a `.env.example` file documenting required variable names without real values.
- Validate environment variables at application startup using schema validation (e.g., Zod), ensuring the process fails immediately if critical secrets are missing.

---

## 4. Mandatory Security Headers

Ensure every HTTP response includes standard hardening headers:
```http
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 0
Referrer-Policy: strict-origin-when-cross-origin
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

---

## 5. Pre-Merge Security Checklist

- [ ] Are all inputs validated against strict schemas (types, formats, lengths)?
- [ ] Is resource ownership (IDOR check) verified on every query and mutation?
- [ ] Are database queries 100% parameterized?
- [ ] Are sensitive endpoints protected by rate limiting?
- [ ] Do error responses hide internal stack traces and server details?
- [ ] Are all secrets stored in environment variables, with no leaks in code?
