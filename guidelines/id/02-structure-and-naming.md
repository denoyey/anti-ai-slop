# 02. Directory Structure & Naming Conventions Standard

[English](../02-structure-and-naming.md) | [Bahasa Indonesia](02-structure-and-naming.md)

---

Dokumen ini mengatur struktur direktori dan konvensi penamaan file/folder agar arsitektur proyek tetap bersih, mudah dirawat (*maintainable*), mudah dicari (*discoverable*), dan tidak menghasilkan penumpukan file liar hasil generate AI.

---

## 1. Konvensi Penamaan (Naming Conventions)

AI wajib mengikuti konvensi baku penamaan berikut secara konsisten tanpa variasi acak:

| Tipe Entitas | Konvensi | Contoh yang Benar | Contoh yang DILARANG |
| :--- | :--- | :--- | :--- |
| **Folder / Direktori** | `kebab-case` atau `snake_case` (seragam di seluruh repo) | `user-management/`, `auth-service/` | `UserManagement/`, `authService/`, `User_mgmt/` |
| **File Kode Biasa** | `kebab-case` | `user-repository.ts`, `auth-controller.py` | `UserRepository.ts`, `user_repo_v2.py` |
| **File Kelas / Komponen UI** | `PascalCase` (khusus JSX/TSX/Vue) atau `kebab-case` | `UserProfileCard.tsx` atau `user-profile-card.tsx` | `userProfileCard.tsx`, `card2.tsx` |
| **File Interface / Type** | `kebab-case` + akhiran deskriptif | `user.types.ts`, `auth-contract.interface.ts` | `IUser.ts`, `types.ts` (terlalu ambigu) |
| **File Unit / Integration Test** | `[nama-file].test.[ext]` atau `[nama-file].spec.[ext]` | `auth-service.test.ts`, `payment_gateway_test.py` | `test.py`, `auth_test2.py` |
| **Nama Variabel / Fungsi** | `camelCase` / `snake_case` (sesuai bahasa) | `calculateTotalAmount()`, `user_payload` | `calc()`, `temp1`, `data`, `res2` |
| **Nama Kelas / Interface** | `PascalCase` | `PostgresUserRepository`, `PaymentProcessor` | `user_repo`, `payment_cls` |
| **Nama Konstanta Global** | `UPPER_SNAKE_CASE` | `MAX_RETRY_ATTEMPTS`, `JWT_SECRET_KEY` | `maxRetry`, `secret` |

### ⛔ Aturan Larangan Keras Nama File:
- **Dilarang keras membuat file dengan embel-embel:** `_v2`, `_new`, `_final`, `_backup`, `_temp`, `_copy`.
- **Dilarang keras nama file ambigu generic:** `utils.ts`, `helper.js`, `common.py`, `data.json` tanpa prefix domain yang jelas (gunakan `string-formatter.util.ts`, `date-parser.util.ts`, `auth-helper.py`).
- **Dilarang menaruh file di root directory** secara sembarangan selain file konfigurasi standar (`README.md`, `PRD.md`, `.gitignore`, `package.json`, dll.).

---

## 2. Pola Arsitektur Folder yang Dianjurkan

Gunakan salah satu dari dua pendekatan terstruktur berikut (sesuai skala proyek):

### Pendekatan A: Feature-Based / Domain-Driven (Sangat Disarankan untuk Skala Menengah-Besar)
Struktur diatur berdasarkan **fitur/domain bisnis**, bukan berdasarkan tipe file teknis semata:

```text
src/
├── core/                           # Inti sistem (shared cross-domain)
│   ├── config/                     # Konfigurasi environment & app
│   ├── database/                   # Migrasi, koneksi DB pool
│   ├── errors/                     # Custom application errors
│   ├── middleware/                 # Global middleware (auth, rate-limit, logger)
│   └── utils/                      # Utilities murni tanpa state
├── modules/                        # Fitur domain terisolasi
│   ├── auth/                       # Domain Auth
│   │   ├── dto/                    # Data Transfer Objects / schemas
│   │   ├── entities/               # Model / Entity database
│   │   ├── repositories/           # Akses query database
│   │   ├── services/               # Logic bisnis inti
│   │   ├── controllers/            # Entry point HTTP / gRPC / CLI
│   │   ├── auth.constants.ts       # Konstanta lokal domain
│   │   └── tests/                  # Unit & integration test auth
│   └── billing/                    # Domain Billing
│       ├── dto/
│       ├── services/
│       └── repositories/
└── main.ts                         # Bootstrap entry point aplikasi
```

### Pendekatan B: Clean Architecture / Hexagonal (Untuk Backend Kompleks)
Memisahkan concern menjadi lingkaran domain:

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

### Pendekatan C: Frontend Architecture (Komponen & State)
```text
src/
├── assets/                         # Font, icon SVG, gambar statis
├── components/                     # Atomic, reusable UI components murni
│   ├── ui/                         # Base design system (Button, Dialog, Input)
│   └── feedback/                   # Toast, Skeleton, Spinner
├── features/                       # Fitur-fitur halaman
│   └── user-profile/
│       ├── components/             # Komponen khusus halaman ini
│       ├── hooks/                  # Custom hooks / business logic
│       ├── services/               # API calls untuk user profile
│       ├── types/                  # TypeScript definitions
│       └── UserProfilePage.tsx     # View entry point
├── layouts/                        # Header, Sidebar, Footer wrappers
├── hooks/                          # Global reusable hooks
├── stores/                         # Global state management
└── styles/                         # Design tokens, variables, global CSS
```

---

## 3. Prinsip Co-Location (Letakkan yang Terkait Berdampingan)

- **Test Berdampingan:** Tempatkan file unit test di samping file implementasinya atau di dalam folder `tests/` di modul yang bersangkutan (misal: `user-service.ts` berdampingan dengan `user-service.test.ts`).
- **Styles & Types:** Komponen frontend yang memiliki style atau tipe data spesifik harus meletakkan file pendukung tersebut di folder yang sama, bukan membuangnya ke folder global antah berantah.

---

## 4. Barrel Files (`index.ts` / `__init__.py`) Guidelines

- Gunakan barrel file (`index.ts`) hanya di batas modul publik (*public API boundaries*) untuk menyederhanakan import.
- **Dilarang:** Membuat circular dependency akibat barrel file yang mengimpor satu sama lain secara bertingkat.
- Pastikan modul mengekspor hanya apa yang dibutuhkan oleh modul luar (*encapsulated module exports*).