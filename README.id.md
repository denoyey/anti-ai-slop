# 🛡️ Standar Rekayasa AI Human-Crafted (`anti-ai-slop`)

🌐 [English](README.md) | **Bahasa Indonesia**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub Repository](https://img.shields.io/badge/GitHub-denoyey%2Fanti--ai--slop-blue?logo=github)](https://github.com/denoyey/anti-ai-slop)
[![Standards: Zero-Slop](https://img.shields.io/badge/Standard-Anti--AI--Slop-success)](guidelines/id/04-anti-ai-slop-design-system.md)

> **Standar Arsitektur, Keamanan Penuh, Desain Berkelanjutan, dan Aturan Operasional Universal untuk AI Coding Assistants (Google Antigravity, Claude Code, Cursor, Windsurf, Copilot, ChatGPT).**

---

## 💡 Apa Ini Sebenarnya? (Penjelasan 30 Detik)

Ini **BUKAN** package `npm` atau library kode yang perlu di-install.

Ini adalah **rulebook dan konfigurasi pagar pengaman (*guardrails*) siap pakai** yang cukup Anda salin ke dalam repositori proyek Anda. Begitu file-file aturan ini berada di proyek Anda, asisten AI (Cursor, Claude Code, Antigravity, Copilot, Windsurf) akan otomatis membacanya dan bertindak sebagai **Senior Principal Software Engineer & Lead Product Designer**—menghilangkan kode rapuh, celah keamanan fatal, dan desain klise "AI Slop".

| Aspek | ❌ Tanpa Standar Ini (AI Slop Biasa) | ✅ Dengan Standar Ini (Karya Manusiawi) |
| :--- | :--- | :--- |
| **Arsitektur Kode** | File monolitik 600 baris, procedural spaghetti | OOP bersih, SOLID, modul domain terisolasi (<300 baris) |
| **Keamanan** | String query SQL langsung, tanpa cek IDOR, secret bocor | 100% parameterized query, validasi zero-trust di backend |
| **Desain UI/UX** | Gradien ungu neon klise, kartu glassmorphism buram | 8-pt grid terukur, mematuhi design token, 5 state UI lengkap |
| **Dokumentasi** | README basi, `.env.example` hilang, API tak terdokumentasi | README dan env tersinkronisasi otomatis di setiap perubahan |
| **Keandalan** | Menelan error (`catch {}` kosong), klaim sukses palsu | Custom domain exception, structured logging, uji test nyata |

---

## ⚡ Cara Menggunakan di Proyek Anda (Pilih AI Tool Anda)

Anda tidak perlu merombak proyek Anda. Cukup salin file yang sesuai dengan AI asisten yang Anda gunakan ke root proyek Anda:

### 1. Cursor IDE (`.cursorrules`)
1. Salin file [`.cursorrules`](.cursorrules) ke root proyek Anda.
2. Salin folder [`guidelines/`](guidelines/) ke root proyek Anda.
3. *Selesai!* Cursor akan otomatis mematuhi aturan ini setiap kali melakukan generate kode.

### 2. Google Antigravity
1. Salin folder [`.antigravity/rules/`](.antigravity/rules/) ke workspace Anda.
2. Salin folder [`guidelines/`](guidelines/) ke workspace Anda.
3. *Selesai!* Antigravity akan membaca dan menegakkan aturan ini pada background task dan subagent.

### 3. Claude Code CLI (`CLAUDE.md`)
1. Salin file [`CLAUDE.md`](CLAUDE.md) ke root proyek Anda.
2. Salin folder [`guidelines/`](guidelines/) ke root proyek Anda.
3. *Selesai!* Claude Code CLI otomatis membaca `CLAUDE.md` saat sesi dimulai.

### 4. Agen AI Universal (Windsurf, Copilot, ChatGPT, dll.)
1. Salin file [`AGENTS.md`](AGENTS.md) ke root proyek Anda.
2. Sebut `@AGENTS.md` pada prompt atau pengaturan sistem Anda.

---

## 🚀 6 Pilar Utama Standar Ini

Klik tautan di bawah ini untuk membaca spesifikasi teknis lengkapnya:

### 1. [Clean OOP & Reusable Architecture](guidelines/id/01-oop-and-reusability.md)
*Menegakkan 4 pilar OOP, prinsip SOLID, Dependency Injection, dan batas maksimal 300 baris per file untuk mencegah God Object.*

### 2. [Predictable Directory & Naming Standard](guidelines/id/02-structure-and-naming.md)
*Menyeragamkan penamaan `kebab-case`, melarang sufiks ambigu (`_v2`, `_temp`, `test2`), dan menyediakan arsitektur Feature-Based & Clean Architecture.*

### 3. [Hardened Security & Anti-Bypass Standard](guidelines/id/03-hardened-security.md)
*Menegakkan Zero-Trust: 100% parameterized query, validasi kepemilikan resource (IDOR/BOLA) di backend, rate limiting, dan nol rahasia di git.*

### 4. [Human-Crafted UI & Anti-AI Slop Design System](guidelines/id/04-anti-ai-slop-design-system.md)
*Melarang desain klise AI (gradien ungu neon, glassmorphism buram). Menegakkan design token, skala 8-pt grid, dan 5 state UI wajib (Default, Skeleton, Empty, Error, Disabled).*

### 5. [Living Documentation & Project Sync Standard](guidelines/id/05-documentation-and-lifecycle-sync.md)
*Aturan Emas: Kode dan dokumentasi adalah satu kesatuan. Setiap perubahan env, dependensi, atau endpoint WAJIB memperbarui `README.md` dan `.env.example` di giliran yang sama.*

### 6. [Error Handling, Logging, and Verification Standard](guidelines/id/06-error-handling-and-testing.md)
*Melarang blok `catch {}` kosong, menerapkan JSON structured logging dengan sensor data sensitif (PII), dan mewajibkan verifikasi nyata via test runner / linter.*

---

## 📁 Struktur Repositori

```text
.
├── README.md                          # 🌐 Dokumentasi Utama (Bahasa Inggris)
├── README.id.md                       # 🇮🇩 Dokumentasi Utama (Bahasa Indonesia)
├── AGENTS.md                          # Instruksi universal untuk semua AI model
├── CLAUDE.md                          # Konfigurasi khusus Claude Code CLI
├── .cursorrules                       # Konfigurasi langsung untuk Cursor IDE
├── PRD_GLOBAL.md                      # Blueprint PRD Global (Bahasa Inggris)
├── PRD_GLOBAL.id.md                   # Blueprint PRD Global (Bahasa Indonesia)
├── .antigravity/
│   └── rules/
│       └── anti-slop.md               # Aturan untuk Google Antigravity
├── guidelines/                        # 🌐 Panduan Standar Utama (Bahasa Inggris)
│   ├── 01-oop-and-reusability.md
│   ├── 02-structure-and-naming.md
│   ├── 03-hardened-security.md
│   ├── 04-anti-ai-slop-design-system.md
│   ├── 05-documentation-and-lifecycle-sync.md
│   └── 06-error-handling-and-testing.md
└── guidelines/id/                     # 🇮🇩 Panduan Standar (Bahasa Indonesia)
    ├── 01-oop-and-reusability.md
    ├── 02-structure-and-naming.md
    ├── 03-hardened-security.md
    ├── 04-anti-ai-slop-design-system.md
    ├── 05-documentation-and-lifecycle-sync.md
    └── 06-error-handling-and-testing.md
```

---

## ❓ Pertanyaan yang Sering Diajukan (FAQ)

<details>
<summary><b>1. Apakah ini bisa dipakai untuk semua bahasa pemrograman dan framework?</b></summary>
<br>
<b>Bisa.</b> Prinsip Clean OOP, SOLID, Zero-Trust security, penamaan semantik, 8-pt grid UI, dan error handling bersifat universal. Standar ini berlaku sama untuk TypeScript, Python, Go, Rust, Java, PHP/Laravel, React, Next.js, Vue, dan lainnya.
</details>

<details>
<summary><b>2. Apakah ini akan menghabiskan banyak token LLM?</b></summary>
<br>
<b>Tidak.</b> File entrypoint (`.cursorrules`, `CLAUDE.md`, `AGENTS.md`) sangat ringkas (~30 baris) dan bertindak sebagai indeks. AI modern hanya akan membaca modul panduan detail di <code>guidelines/</code> saat mengerjakan tugas yang relevan.
</details>

<details>
<summary><b>3. Bisakah saya menyesuaikan aturan ini untuk standar tim saya sendiri?</b></summary>
<br>
<b>Tentu saja.</b> Fork atau clone repositori ini, sesuaikan isi file di dalam folder <code>guidelines/</code> dengan standar internal tim Anda, dan simpan sebagai template proyek Anda.
</details>

---

## 📄 Lisensi & Pemelihara

Proyek ini dilisensikan di bawah lisensi MIT — lihat file [LICENSE](LICENSE) untuk detail lengkap.

Dibuat dan dikelola oleh **denoyey** ([@denoyey](https://github.com/denoyey)).
