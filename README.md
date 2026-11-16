# 🛡️ Human-Crafted AI Engineering Standard (`anti-ai-slop`)

🌐 **English** | [Bahasa Indonesia](README.id.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub Repository](https://img.shields.io/badge/GitHub-denoyey%2Fanti--ai--slop-blue?logo=github)](https://github.com/denoyey/anti-ai-slop)
[![Standards: Zero-Slop](https://img.shields.io/badge/Standard-Anti--AI--Slop-success)](guidelines/04-anti-ai-slop-design-system.md)

> **Production-grade architecture, hardened zero-trust security, human-crafted design, and universal operational guardrails for AI coding assistants (Google Antigravity, Claude Code, Cursor, Windsurf, Copilot, ChatGPT).**

---

## 📌 Why This Repository Exists

Modern AI coding assistants frequently produce what the software industry terms **"AI Slop"**:
- Random procedural scripts (*spaghetti code*) devoid of proper OOP design or domain boundaries.
- Fragile, unmaintainable folder structures with haphazard file naming (`test_new2.js`, `utils_v2.py`, `temp_data.ts`).
- Critical security vulnerabilities: unparameterized database queries, missing IDOR/BOLA authorization checks, secrets leaked in git commits, and nonexistent rate limiting.
- Cheap, generic aesthetics: ubiquitous purple-blue neon gradients, unreadable glassmorphic cards, and components lacking realistic state handling (*skeletons, empty states, error recovery*).
- Stale documentation: AI agents modifying dependencies, endpoints, or environment variables without updating `README.md` or configuration templates.

This repository serves as a **battle-tested rulebook and production guardrail framework** that enforces AI agents to operate at the level of a **Senior Principal Software Engineer & Lead Product Designer**.

---

## ⚡ Quick Start / Clone

To adopt this standard across your project or workflow:

```bash
git clone https://github.com/denoyey/anti-ai-slop.git
```

Alternatively, copy the relevant configuration files (`.antigravity/`, `.cursorrules`, `CLAUDE.md`, `AGENTS.md`) along with the `guidelines/` directory directly into your repository root.

---

## 📁 Repository Structure

```text
.
├── .antigravity/
│   └── rules/
│       └── anti-slop.md            # Automated rules for Google Antigravity
├── guidelines/                     # Core standards in English
│   ├── 01-oop-and-reusability.md   # Clean OOP, SOLID principles, & reusability
│   ├── 02-structure-and-naming.md  # Predictable naming conventions & architecture
│   ├── 03-hardened-security.md     # Defense-in-depth security (OWASP & anti-bypass)
│   ├── 04-anti-ai-slop-design-system.md # Human-crafted UI design, no generic slop
│   ├── 05-documentation-and-lifecycle-sync.md # Mandatory docs & README sync rule
│   ├── 06-error-handling-and-testing.md # Zero silent failures & real verification
│   └── id/                         # Standards in Bahasa Indonesia
├── .cursorrules                    # Direct configuration for Cursor IDE
├── AGENTS.md                       # Universal agent instruction standard
├── CLAUDE.md                       # Dedicated configuration for Claude Code CLI
├── PRD_GLOBAL.md                   # Global PRD blueprint (English)
├── PRD_GLOBAL.id.md                # Global PRD blueprint (Bahasa Indonesia)
├── README.md                       # Main project documentation (English)
└── README.id.md                    # Main project documentation (Bahasa Indonesia)
```

---

## 🚀 The 6 Core Pillars

### 1. [Clean OOP & Reusable Architecture](guidelines/01-oop-and-reusability.md)
- Core OOP Pillars (Encapsulation, Abstraction, Polymorphism, Favor Composition over Inheritance).
- Strict 100% adherence to **SOLID** principles.
- Strict ban on God Objects / God Classes. Maximum 300 lines per file.
- Contract-first design using Interfaces/DTOs and Dependency Injection (DI).

### 2. [Predictable Directory & Naming Standard](guidelines/02-structure-and-naming.md)
- Consistent `kebab-case` convention across directories and non-UI code files.
- Strict ban on ambiguous suffixes: `_v2`, `_new`, `_backup`, `temp`.
- Clear architectural choices: *Feature-Based* or *Clean / Hexagonal Architecture*.
- *Co-location Principle*: Keep tests, types, and styles adjacent to their respective features.

### 3. [Hardened Security & Anti-Bypass](guidelines/03-hardened-security.md)
- **Zero-Trust:** Validate and sanitize all inputs server-side using strict schema validators (Zod/Pydantic).
- **100% Parameterized Queries:** Total immunity against SQL, NoSQL, and Command Injections.
- **Anti-IDOR / Anti-BOLA:** Enforce server-side ownership verification on every data query and mutation.
- **Secrets Protection:** Zero credentials in git; fail-fast validation of environment variables on startup.
- **Defense in Depth:** Rate limiting on auth endpoints, secure cookie attributes, anti-SSRF protections, magic-bytes file upload verification, and DoS mitigation.

### 4. [Human-Crafted UI & Anti-AI Slop Design](guidelines/04-anti-ai-slop-design-system.md)
- Strict ban on generic purple-blue gradients, excessive glassmorphic blur, and decorative floating icon pills.
- 100% compliance with existing design tokens and standard 8-point grid spacing.
- **5 Complete UI States**: Default, Skeleton Loading, Empty State, Error State (with retry action), and Disabled State.
- Human copywriting: Direct, concise, functional, and free of hyperbolic AI buzzwords.

### 5. [Living Documentation & Sync Protocol](guidelines/05-documentation-and-lifecycle-sync.md)
- **Golden Rule:** Code and documentation are an inseparable unit.
- Whenever an AI introduces new environment variables, dependencies, or API endpoints, it **MUST** update `README.md` and `.env.example` in the same turn before concluding its work.

### 6. [Zero Silent Failures & Rigorous Verification](guidelines/06-error-handling-and-testing.md)
- Strict ban on empty catch blocks (`try {} catch {}`).
- Structured JSON logging with automatic PII (Personally Identifiable Information) masking.
- Empirical verification: AI must run test runners / linters / typechecks before claiming that a feature works.

---

## 🛠️ How to Use in Your Project

### Option A: Google Antigravity
Copy the `.antigravity/rules/` and `guidelines/` directories to your workspace root. Antigravity will automatically load and enforce these rules.

### Option B: Cursor IDE
Copy `.cursorrules` and the `guidelines/` directory to your repository root.

### Option C: Claude Code CLI
Copy `CLAUDE.md` and the `guidelines/` directory to your repository root.

### Option D: Universal AI Assistants (Windsurf, Copilot, ChatGPT, etc.)
Use `AGENTS.md` as the primary instruction file in your repository root.

---

## 📋 [Global PRD Blueprint](PRD_GLOBAL.md)
Use `PRD_GLOBAL.md` as a baseline specification before building new features to prevent AI hallucination, feature creep, and architectural drift.

---

## 📄 License & Maintainer

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for full details.

Crafted and maintained by **denoyey** ([@denoyey](https://github.com/denoyey)).
