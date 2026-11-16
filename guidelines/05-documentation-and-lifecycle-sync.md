# 05. Living Documentation & Project Lifecycle Sync Standard

[English](05-documentation-and-lifecycle-sync.md) | [Bahasa Indonesia](id/05-documentation-and-lifecycle-sync.md)

---

This document establishes a mandatory rule: **Code and Documentation are an inseparable unit**. AI coding assistants are strictly prohibited from altering project code without synchronizing documentation and the `README.md` file.

---

## 1. The Living Documentation Rule

Whenever any change occurs (feature addition, refactoring, dependency updates, bug fixes, or configuration tweaks), the AI agent **MUST** update all corresponding documentation:

### Trigger & Update Matrix:

| Type of Code Change | Mandatory Documentation Updates |
| :--- | :--- |
| **New or Changed Environment Variable** | 1. `.env.example`<br>2. Environment Variables table in `README.md` |
| **New or Removed Library Dependency** | 1. Installation instructions in `README.md`<br>2. Justification in PRD / Changelog |
| **New API Endpoint or Schema Change** | 1. API documentation (OpenAPI / Swagger or `docs/api.md`)<br>2. Usage examples in `README.md` |
| **Directory Structure or Architecture Shift** | 1. Repository tree in `README.md`<br>2. Relevant architecture guidelines |
| **Completed Feature from PRD** | 1. Task checklist in `PRD_GLOBAL.md`<br>2. Feature matrix in `README.md` |
| **Security Patch or Fix** | 1. Release notes in `CHANGELOG.md` |

---

## 2. Standards for Maintaining `README.md`

`README.md` is the primary storefront of the repository. Keep it perpetually accurate:
1. **Installation & Running Instructions:** Must be verified and accurate. If new commands are introduced (migrations, seeds, key generation), list them sequentially.
2. **System Prerequisites:** Explicitly state supported runtimes (Node.js, Python, Go, Docker, PostgreSQL versions).
3. **Environment Variable Documentation:** Every key in `.env.example` must have an explanation and a safe dummy value in `README.md`.

---

## 3. Pre-Completion Documentation Verification Protocol

Before an AI assistant declares a task finished or returns its final response to the user, it must evaluate this internal checklist:

```markdown
[ ] Were new files added or paths moved? -> Update tree in README.
[ ] Were new environment variables introduced? -> Update .env.example and README.
[ ] Were new setup commands added? -> Update Quick Start in README.
[ ] Were PRD items completed? -> Check off items in PRD_GLOBAL.md.
[ ] Are API docs synchronized with current endpoint implementations?
```

If any check is incomplete, the AI assistant must update documentation before concluding its turn.

---

## 4. Conventional Commits Standard

Use the **Conventional Commits** specification for all summaries and commit messages:
- `feat(auth): add rate limiting and argon2 password hashing`
- `fix(billing): prevent IDOR vulnerability in invoice download endpoint`
- `docs(readme): update environment variable table for OAuth setup`
- `refactor(user): decouple repository from controller using dependency injection`
- `test(security): add test suite for SQL injection prevention`
