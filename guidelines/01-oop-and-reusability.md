# 01. Object-Oriented Programming (OOP) & Code Reusability Standard

[English](01-oop-and-reusability.md) | [Bahasa Indonesia](id/01-oop-and-reusability.md)

---

This document defines non-negotiable rules for all AI coding assistants (Google Antigravity, Claude Code, Cursor, Copilot, ChatGPT, etc.) when designing, writing, and refactoring code in this repository.

---

## 1. Core Philosophy: Clean & Modular OOP

AI-generated code must NEVER consist of procedural spaghetti, monolithic giant functions, or disorganized scripts. Code must be structured, testable, extensible, and enforce strict domain boundaries.

### The 4 Mandatory OOP Pillars:
1. **Encapsulation:**
   - Hide internal state. Strictly enforce access modifiers (`private`, `protected`).
   - Never expose raw mutable internal variables. Use explicit methods that validate state transitions.
2. **Abstraction:**
   - Decouple contracts/interfaces from concrete implementations.
   - Code consumers must depend on interface contracts, not on internal implementation details.
3. **Inheritance vs. Composition:**
   - **Golden Rule:** *Favor composition over inheritance*.
   - Avoid inheritance hierarchies deeper than 2 levels (`Class A -> Class B -> Class C` is the absolute limit).
   - Use dependency injection and delegation to share behavior, not rigid subclassing.
4. **Polymorphism:**
   - Replace complex `switch-case` blocks or nested `if-else` type-checking ladders with polymorphic behavior.
   - Leverage the *Strategy Pattern* or *Factory Pattern* for dynamic runtime execution.

---

## 2. Strict Adherence to SOLID Principles

Every class and module must strictly observe all 5 SOLID principles:

### S – Single Responsibility Principle (SRP)
- Every class must have **only one reason to change**.
- *Forbidden:* "God Objects" or "God Classes" (e.g., a `UserManager` handling authentication, DB queries, sending emails, and rendering UI views).
- *Solution:* Split into `AuthService`, `UserRepository`, `EmailNotifier`, and `UserPresenter`.

### O – Open/Closed Principle (OCP)
- Software entities must be **open for extension, but closed for modification**.
- Adding new features (e.g., a new payment gateway, export format) should not require altering existing core code; introduce a new class implementing the shared interface instead.

### L – Liskov Substitution Principle (LSP)
- Subtypes must be substitutable for their base types without breaking application behavior.
- Never throw `NotImplementedException` in a subclass simply because it does not need a method from the base interface (a clear violation of ISP and LSP).

### I – Interface Segregation Principle (ISP)
- Prefer multiple, client-specific interfaces over a single, bloated (*fat*) interface.
- Clients must never be forced to depend on methods they do not use.

### D – Dependency Inversion Principle (DIP)
- High-level modules must not depend on low-level modules; both must depend on abstractions.
- Apply **Dependency Injection (DI)**: Never instantiate dependencies directly inside business classes (`new Service()`). Inject instances via constructor parameters.

---

## 3. Production Code Reusability Standards

Reusable code does not mean over-abstracted code. Follow these practical rules:

1. **Rule of Three:**
   - Do not create generic abstractions until logic is duplicated in at least 2 to 3 distinct locations. Avoid premature abstraction.
2. **Pure Functions & Stateless Utilities:**
   - Helper utilities should be pure functions whenever possible: identical inputs always yield identical outputs without side effects or reliance on global state.
3. **Data Transfer Objects (DTO) & Typed Contracts:**
   - Data transfer across boundaries (Controller -> Service -> Repository) must use strictly typed schemas or DTOs, never untyped dictionaries, `any`, or unstructured payloads.
4. **Atomic Components (Frontend):**
   - Break UI into granular atomic components: Button, Input, Modal, Typography.
   - Separate *Container/Smart Components* (data fetching & business state) from *Presentational/Dumb Components* (pure visual rendering).

---

## 4. Recommended Design Patterns

Apply industry-standard design patterns based on context:

| Design Pattern | When to Use | Typical Example |
| :--- | :--- | :--- |
| **Repository Pattern** | Decoupling domain logic from data access/database | `UserRepositoryInterface` -> `PostgresUserRepository` |
| **Strategy Pattern** | Interchangeable business algorithms at runtime | Discount rules, payment providers (Stripe, PayPal) |
| **Factory / Builder** | Complex object instantiation with many options | Query builders, multi-channel notification builders |
| **Adapter Pattern** | Isolating third-party libraries from core code | Wrapping HTTP clients (Axios, Fetch, Requests) |
| **Observer / Event-Driven** | Decoupled cross-domain signaling | `UserRegisteredEvent` handled by `SendWelcomeEmailListener` |

---

## 5. Strict Prohibitions for AI Agents:

❌ **Files exceeding 300 lines** without modular separation.  
❌ **Mutable global state** modified across arbitrary code paths.  
❌ **Hardcoded business rules** placed in presentation/UI layers.  
❌ **Copy-paste duplication** across validation logic, data transformations, or queries.  
❌ **Untyped escapes**: Using `any`, `object`, or loose type casting to bypass type checkers.
