# 🛡️ Standar Rekayasa AI Human-Crafted (`anti-ai-slop`)

🌐 [English](README.md) | **Bahasa Indonesia**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub Repository](https://img.shields.io/badge/GitHub-denoyey%2Fanti--ai--slop-blue?logo=github)](https://github.com/denoyey/anti-ai-slop)
[![Standards: Zero-Slop](https://img.shields.io/badge/Standard-Anti--AI--Slop-success)](guidelines/id/04-anti-ai-slop-design-system.md)

> **Standar Arsitektur, Keamanan Penuh, Desain Berkelanjutan, dan Aturan Operasional Universal untuk AI Coding Assistants (Google Antigravity, Claude Code, Cursor, Windsurf, Copilot, ChatGPT).**

---

## 📌 Mengapa Repositori Ini Dibuat?

Model AI sering kali menghasilkan apa yang disebut **"AI Slop"**:
- Kode prosedural acak (*spaghetti code*) tanpa paradigma OOP yang benar.
- Kode yang sulit di-maintain dengan penamaan file acak (`test_new2.js`, `utils_v2.py`).
- Celah keamanan fatal: tidak ada pengecekan IDOR/BOLA, query SQL tanpa parameterisasi, secret bocor di kode, dan tanpa rate-limiting.
- Desain visual murahan: gradien neon ungu-biru klise, efek blur kaca tak terbaca, dan tombol tanpa handling *loading/empty/error states*.
- Dokumentasi dan `README.md` yang basi karena AI mengubah kode tanpa pernah memperbarui dokumentasinya.

Repositori ini hadir sebagai **rulebook dan pagar pengaman (*guardrails*) produksi** agar semua AI asisten bekerja dengan standar **Senior Principal Software Engineer & Lead Human Designer**.

---

## ⚡ Quick Start / Clone

Untuk mengadopsi standar ini ke dalam workflow atau proyek Anda:

```bash
git clone https://github.com/denoyey/anti-ai-slop.git
```

Atau salin file konfigurasi yang relevan (`.antigravity/`, `.cursorrules`, `CLAUDE.md`, `AGENTS.md`) beserta folder `guidelines/` ke repositori proyek Anda.

---

## 📁 Struktur Repositori

```text
.
├── .antigravity/
│   └── rules/
│       └── anti-slop.md            # Aturan otomatis untuk Google Antigravity
├── guidelines/                     # Panduan Standar Utama (Bahasa Inggris)
│   ├── 01-oop-and-reusability.md   # Prinsip OOP, SOLID, & reusable patterns
│   ├── 02-structure-and-naming.md  # Konvensi penamaan & arsitektur folder
│   ├── 03-hardened-security.md     # Keamanan berlapis (OWASP, anti-bypass)
│   ├── 04-anti-ai-slop-design-system.md # Desain buatan manusia, no generic slop
│   ├── 05-documentation-and-lifecycle-sync.md # Wajib sync docs & README
│   ├── 06-error-handling-and-testing.md # Zero silent fail & testing
│   └── id/                         # Panduan dalam Bahasa Indonesia
├── .cursorrules                    # Konfigurasi langsung untuk Cursor IDE
├── AGENTS.md                       # Standar instruksi universal semua agent
├── CLAUDE.md                       # Konfigurasi khusus Claude Code CLI
├── PRD_GLOBAL.md                   # PRD Global standar & blueprint sistem
├── PRD_GLOBAL.id.md                # PRD Global dalam Bahasa Indonesia
├── README.md                       # Dokumentasi utama (English)
└── README.id.md                    # Dokumentasi utama (Bahasa Indonesia)
```

---

## 🚀 6 Pilar Utama Standar Ini

### 1. [Clean OOP & Reusable Architecture](guidelines/id/01-oop-and-reusability.md)
- 4 Pilar OOP (Encapsulation, Abstraction, Polymorphism, Utamakan Composition daripada Inheritance).
- Kepatuhan 100% pada prinsip **SOLID**.
- Dilarang membuat God Object / God Class. Maksimal panjang file 300 baris.
- Terapkan Dependency Injection (DI) dan arsitektur berbasis kontrak (Interface/DTO).

### 2. [Predictable Directory & Naming Standard](guidelines/id/02-structure-and-naming.md)
- Standar penamaan folder dan file seragam menggunakan `kebab-case`.
- Larangan keras membuat file dengan sufiks ambigu: `_v2`, `_new`, `_backup`, `temp`.
- Pilihan arsitektur modular yang jelas: *Feature-Based* atau *Clean Architecture*.
- Prinsip *Co-location*: letakkan test dan style berdampingan dengan unit fiturnya.

### 3. [Hardened Security & Anti-Bypass](guidelines/id/03-hardened-security.md)
- **Zero-Trust:** Validasi semua input di server menggunakan strict schema.
- **100% Parameterized Queries:** Anti SQL/NoSQL Injection.
- **Anti-IDOR / Anti-BOLA:** Validasi hak kepemilikan resource di setiap aksi mutating/query.
- **Secrets Protection:** Zero credential di git; validasi startup env wajib ada.
- **Defense in Depth:** Rate limiting di auth, secure cookie headers, anti-SSRF, magic-bytes file upload validation, mitigasi DoS.

### 4. [Human-Crafted UI & Anti-AI Slop Design](guidelines/id/04-anti-ai-slop-design-system.md)
- Dilarang menggunakan gradien ungu neon generik, glassmorphism buram, dan ikon lingkaran hiasan acak.
- Patuh 100% pada design tokens dan skala 8-pt grid yang sudah ada dalam proyek.
- Wajib memiliki **5 State Antarmuka Lengkap**: Default, Skeleton Loading, Empty State, Error State (dengan aksi retry), dan Disabled State.
- Copywriting manusiawi: tidak menggunakan kalimat hiperbolis klise AI.

### 5. [Living Documentation & Sync Protocol](guidelines/id/05-documentation-and-lifecycle-sync.md)
- **Aturan Mutlak:** Kode dan dokumentasi adalah satu kesatuan.
- Setiap kali AI mengubah environment variables, dependensi, atau endpoint API, AI **WAJIB** memperbarui file `README.md` dan `.env.example` sebelum menyelesaikan tugas.

### 6. [Zero Silent Failures & Rigorous Verification](guidelines/id/06-error-handling-and-testing.md)
- Dilarang menelan error secara diam-diam (`try {} catch {}` kosong).
- Logging terstruktur tanpa membocorkan PII (Personally Identifiable Information).
- Verifikasi nyata: AI harus menguji kode dengan test runner / linter sebelum menyatakan selesai.

---

## 🛠️ Cara Menggunakan di Proyek Anda

### Opsi A: Menggunakan dengan Google Antigravity
Salin folder `.antigravity/rules/` dan folder `guidelines/` ke root workspace Anda. Antigravity akan otomatis membaca aturan ini.

### Opsi B: Menggunakan dengan Cursor IDE
Salin file `.cursorrules` dan folder `guidelines/` ke root repositori Anda.

### Opsi C: Menggunakan dengan Claude Code
Salin file `CLAUDE.md` dan folder `guidelines/` ke root repositori Anda.

### Opsi D: Agen AI Universal (Windsurf, Copilot, ChatGPT, dll.)
Gunakan file `AGENTS.md` sebagai file instruksi utama di root repositori.

---

## 📋 [PRD Global Standar](PRD_GLOBAL.id.md)
Gunakan `PRD_GLOBAL.id.md` sebagai blueprint sebelum memulai fitur baru untuk mencegah AI berhalusinasi atau melenceng dari spesifikasi bisnis dan keamanan.

---

## 📄 Lisensi & Pemelihara

Proyek ini dilisensikan di bawah lisensi MIT — lihat file [LICENSE](LICENSE) untuk detail lengkap.

Dibuat dan dikelola oleh **denoyey** ([@denoyey](https://github.com/denoyey)).
