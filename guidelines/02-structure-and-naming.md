# 02. Directory Structure & Naming Conventions Standard

[English](02-structure-and-naming.md) | [Bahasa Indonesia](id/02-structure-and-naming.md)

---

This document establishes predictable directory layouts and naming conventions to ensure the codebase remains clean, maintainable, discoverable, and free of chaotic AI-generated files.

---

## 1. Naming Conventions

AI coding assistants must strictly follow these naming conventions:

| Entity Type | Convention | Correct Example | FORBIDDEN Example |
| :--- | :--- | :--- | :--- |
| **Folders / Directories** | `kebab-case` or `snake_case` (consistent repo-wide) | `user-management/`, `auth-service/` | `UserManagement/`, `authService/`, `User_mgmt/` |
| **Standard Code Files** | `kebab-case` | `user-repository.ts`, `auth-controller.py` | `UserRepository.ts`, `user_repo_v2.py` |
| **UI Components** | `PascalCase` (for JSX/TSX/Vue) or `kebab-case` | `UserProfileCard.tsx` or `user-profile-card.tsx` | `userProfileCard.tsx`, `card2.tsx` |
| **Interfaces / Types** | `kebab-case` + descriptive suffix | `user.types.ts`, `auth-contract.interface.ts` | `IUser.ts`, `types.ts` (too ambiguous) |
| **Test Files** | `[filename].test.[ext]` or `[filename].spec.[ext]` | `auth-service.test.ts`, `payment_gateway_test.py` | `test.py`, `auth_test2.py` |
| **Variables / Functions** | `camelCase` / `snake_case` (language idiomatic) | `calculateTotalAmount()`, `user_payload` | `calc()`, `temp1`, `data`, `res2` |
| **Classes / Interfaces** | `PascalCase` | `PostgresUserRepository`, `PaymentProcessor` | `user_repo`, `payment_cls` |
| **Global Constants** | `UPPER_SNAKE_CASE` | `MAX_RETRY_ATTEMPTS`, `JWT_SECRET_KEY` | `maxRetry`, `secret` |

### ⛔ Strict Prohibitions on Filenames:
- **Never use versioning or temp suffixes:** `_v2`, `_new`, `_final`, `_backup`, `_temp`, `_copy`.
- **Never use ambiguous generic names:** `utils.ts`, `helper.js`, `common.py`, `data.json` without clear domain scoping (prefer `string-formatter.util.ts`, `date-parser.util.ts`, `auth-helper.py`).
- **Never dump random files into the root directory** other than standard project configuration (`README.md`, `PRD.md`, `.gitignore`, `package.json`, etc.).

---

## 2. Recommended Directory Architecture

Select one of the following architectural patterns according to project scale:

### Pattern A: Feature-Based / Domain-Driven (Recommended for Medium to Large Systems)
Organized by **business domain**, rather than technical file types alone:

```text
src/
├── core/                           # System core (shared cross-domain)
│   ├── config/                     # Environment & app configuration
│   ├── database/                   # Migrations, connection pooling
│   ├── errors/                     # Custom domain errors
│   ├── middleware/                 # Global middleware (auth, rate-limit, logger)
│   └── utils/                      # Pure, stateless utilities
├── modules/                        # Isolated domain features
│   ├── auth/                       # Auth domain
│   │   ├── dto/                    # Data Transfer Objects / validation schemas
│   │   ├── entities/               # Database entities / models
│   │   ├── repositories/           # Database queries
│   │   ├── services/               # Core business logic
│   │   ├── controllers/            # HTTP / gRPC / CLI entry points
│   │   ├── auth.constants.ts       # Domain-local constants
│   │   └── tests/                  # Auth unit & integration tests
│   └── billing/                    # Billing domain
│       ├── dto/
│       ├── services/
│       └── repositories/
└── main.ts                         # Application bootstrap entry point
```

### Pattern B: Clean Architecture / Hexagonal (For Complex Backends)
Separates concerns into concentric architectural layers:

```text
src/
├── domain/                         # Enterprise Business Rules (Entities, Value Objects)
│   ├── entities/
│   └── exceptions/
├── application/                    # Application Business Rules (Use Cases, DTOs, Ports)
│   ├── use-cases/
│   └── interfaces/
├── infrastructure/                 # Frameworks & Drivers (DB, External APIs, Cache)
│   ├── persistence/
│   ├── external-services/
│   └── logger/
└── presentation/                   # Adapters (Controllers, CLI, REST API, GraphQL)
    ├── http/
    │   ├── controllers/
    │   └── middlewares/
    └── serializers/
```

### Pattern C: Frontend Component Architecture
```text
src/
├── assets/                         # Fonts, SVG icons, static media
├── components/                     # Pure, reusable UI components
│   ├── ui/                         # Design system primitives (Button, Dialog, Input)
│   └── feedback/                   # Toast, Skeleton, Spinner
├── features/                       # Page-specific feature modules
│   └── user-profile/
│       ├── components/             # Feature-specific components
│       ├── hooks/                  # Custom hooks / view-models
│       ├── services/               # Feature-specific API clients
│       ├── types/                  # Local TypeScript types
│       └── UserProfilePage.tsx     # View entry point
├── layouts/                        # Header, Sidebar, Footer wrappers
├── hooks/                          # Reusable global hooks
├── stores/                         # Global state management
└── styles/                         # Design tokens, CSS variables, global styling
```

---

## 3. Co-Location Principle

- **Co-locate Tests:** Place unit tests adjacent to the implementation file or inside a co-located `tests/` directory within the module (e.g., `user-service.ts` next to `user-service.test.ts`).
- **Co-locate Styles & Types:** Feature-specific styles and types must live within the feature folder, not dumped into global folders.

---

## 4. Barrel File Guidelines (`index.ts` / `__init__.py`)

- Use barrel files exclusively at public module boundaries to simplify external imports.
- **Forbidden:** Creating circular dependencies caused by cross-importing nested barrel files.
- Ensure modules only expose their intended public API (*encapsulated module exports*).
