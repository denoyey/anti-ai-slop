# 🛡️ Human-Crafted AI Engineering Standard (`anti-ai-slop`)

🌐 **English** | [Bahasa Indonesia](README.id.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub Repository](https://img.shields.io/badge/GitHub-denoyey%2Fanti--ai--slop-blue?logo=github)](https://github.com/denoyey/anti-ai-slop)
[![Standards: Zero-Slop](https://img.shields.io/badge/Standard-Anti--AI--Slop-success)](guidelines/04-anti-ai-slop-design-system.md)

> **Production-grade architecture, hardened zero-trust security, human-crafted UI design, and living documentation rules for AI coding assistants (Google Antigravity, Claude Code, Cursor, Windsurf, Copilot, ChatGPT).**

---

## 💡 What is this in 30 Seconds?

This is **NOT** a software library or an npm package. 

It is a **plug-and-play rulebook and guardrail configuration** that you drop into your repository. Once placed in your project root, AI coding assistants (like Cursor, Claude Code, Antigravity, Copilot, and Windsurf) will automatically read these rules and act as a **Senior Principal Software Engineer & Lead Product Designer**—eliminating fragile code, amateur security flaws, and generic "AI Slop" designs.

| Aspect | ❌ Without This Standard (Typical AI Slop) | ✅ With This Standard (Human-Crafted) |
| :--- | :--- | :--- |
| **Code Architecture** | 600-line monolithic files, procedural spaghetti | Clean OOP, SOLID, modular domain services (<300 lines) |
| **Security** | Concatenated SQL strings, missing IDOR checks, leaked secrets | 100% parameterized queries, zero-trust server validation |
| **UI/UX Design** | Generic purple-blue neon gradients, unreadable glassmorphism | Intentional 8-pt grid, existing design tokens, 5 complete UI states |
| **Documentation** | Stale README, missing `.env.example`, undocumented APIs | Automatic sync of README and env specs on every change |
| **Reliability** | Silently swallowed exceptions (`catch {}`), unverified claims | Custom domain errors, structured logs, empirical test verification |

---

## ⚡ How to Use in Your Project (Choose Your AI Tool)

You don't need to rebuild your project. Simply copy the files corresponding to your AI assistant into your existing codebase:

### 1. Cursor IDE (`.cursorrules`)
1. Copy [`.cursorrules`](.cursorrules) to your project root.
2. Copy the [`guidelines/`](guidelines/) folder to your project root.
3. *Done!* Cursor now automatically adheres to these rules for every generation and prompt.

### 2. Google Antigravity
1. Copy the [`.antigravity/rules/`](.antigravity/rules/) folder to your workspace.
2. Copy the [`guidelines/`](guidelines/) folder to your workspace.
3. *Done!* Antigravity reads and enforces the rules in background tasks and subagents.

### 3. Claude Code CLI (`CLAUDE.md`)
1. Copy [`CLAUDE.md`](CLAUDE.md) to your repository root.
2. Copy the [`guidelines/`](guidelines/) folder to your repository root.
3. *Done!* Claude Code CLI reads `CLAUDE.md` automatically at the start of every session.

### 4. Universal Agents (Windsurf, Copilot, ChatGPT, etc.)
1. Copy [`AGENTS.md`](AGENTS.md) to your repository root.
2. Reference `@AGENTS.md` in your prompts or system settings.

---

## 🚀 The 6 Core Pillars

Click each link below to read the comprehensive technical specifications:

### 1. [Clean OOP & Reusable Architecture](guidelines/01-oop-and-reusability.md)
*Enforces 4 pillars of OOP, strict SOLID principles, Dependency Injection, and a 300-line cap per file to prevent "God Objects".*

### 2. [Predictable Directory & Naming Standard](guidelines/02-structure-and-naming.md)
*Enforces uniform `kebab-case` naming, bans ambiguous suffixes (`_v2`, `_temp`, `test2`), and provides Feature-Based and Clean Architecture blueprints.*

### 3. [Hardened Security & Anti-Bypass Standard](guidelines/03-hardened-security.md)
*Enforces Zero-Trust: 100% parameterized queries, mandatory server-side IDOR/BOLA ownership validation, rate limiting, and zero credentials in git.*

### 4. [Human-Crafted UI, Anti-AI Slop & Universal Responsiveness](guidelines/04-anti-ai-slop-design-system.md)
*Bans generic AI clichés (purple neon gradients, unreadable glassmorphism). Enforces strict design tokens, 8-pt spacing, 5 mandatory UI states, and 100% responsiveness from the smallest iPhone (320px) to 4K ultra-wide monitors with native iOS Safe Area (`env()`) & dynamic viewport (`100dvh`) compliance.*

### 5. [Living Documentation & Project Sync Standard](guidelines/05-documentation-and-lifecycle-sync.md)
*Golden Rule: Code and documentation are inseparable. Any change to dependencies, environment variables, or endpoints MUST update `README.md` and `.env.example` in the same turn.*

### 6. [Error Handling, Logging, and Verification Standard](guidelines/06-error-handling-and-testing.md)
*Bans empty `catch {}` blocks, requires structured JSON logging with automatic PII masking, and mandates empirical test runner / linter verification.*

---

## 📁 Repository Structure

```text
.
├── README.md                          # 🌐 English Main Documentation
├── README.id.md                       # 🇮🇩 Indonesian Main Documentation
├── AGENTS.md                          # Universal instruction file for all AI models
├── CLAUDE.md                          # Dedicated configuration for Claude Code CLI
├── .cursorrules                       # Direct configuration for Cursor IDE
├── PRD_GLOBAL.md                      # Global PRD blueprint (English)
├── PRD_GLOBAL.id.md                   # Global PRD blueprint (Bahasa Indonesia)
├── .antigravity/
│   └── rules/
│       └── anti-slop.md               # Rules for Google Antigravity
├── guidelines/                        # 🌐 Core Standard Guidelines (English)
│   ├── 01-oop-and-reusability.md
│   ├── 02-structure-and-naming.md
│   ├── 03-hardened-security.md
│   ├── 04-anti-ai-slop-design-system.md
│   ├── 05-documentation-and-lifecycle-sync.md
│   └── 06-error-handling-and-testing.md
└── guidelines/id/                     # 🇮🇩 Core Standard Guidelines (Bahasa Indonesia)
    ├── 01-oop-and-reusability.md
    ├── 02-structure-and-naming.md
    ├── 03-hardened-security.md
    ├── 04-anti-ai-slop-design-system.md
    ├── 05-documentation-and-lifecycle-sync.md
    └── 06-error-handling-and-testing.md
```

---

## ❓ Frequently Asked Questions (FAQ)

<details>
<summary><b>1. Does this work with any programming language or framework?</b></summary>
<br>
<b>Yes.</b> The principles (Clean OOP, SOLID, Zero-Trust security, semantic naming, 8-pt grid UI, error handling) are universal. They apply equally to TypeScript, Python, Go, Rust, Java, PHP/Laravel, React, Next.js, Vue, and more.
</details>

<details>
<summary><b>2. Will this consume too many LLM tokens?</b></summary>
<br>
<b>No.</b> The entrypoint files (`.cursorrules`, `CLAUDE.md`, `AGENTS.md`) are lightweight index summaries (~30 lines) that link to modular guideline files. Modern agents read detailed guidelines on-demand only when tackling relevant tasks.
</details>

<details>
<summary><b>3. Can I customize or override these rules for my team?</b></summary>
<br>
<b>Absolutely.</b> Fork or clone this repository, adjust the guidelines in <code>guidelines/</code> to match your company's internal conventions, and commit them to your repository template.
</details>

---

## 📄 License & Maintainer

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for full details.

Crafted and maintained by **denoyey** ([@denoyey](https://github.com/denoyey)).
