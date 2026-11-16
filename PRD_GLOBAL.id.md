# PRD Global: Anti-Slop AI Engineering & Design Standard

[English](PRD_GLOBAL.md) | [Bahasa Indonesia](PRD_GLOBAL.id.md)

---

## 1. Ringkasan Eksekutif & Visi Produk (Executive Summary)
Inisiatif ini dirancang untuk mengatasi fenomena **"AI Slop"**—kode, desain, dan struktur proyek murahan, generik, rentan keamanan, dan tidak beraturan yang sering dihasilkan oleh model AI (Antigravity, Claude, Cursor, Copilot, ChatGPT).

Standar ini mengonversi AI dari sekadar "code generator acak" menjadi **Senior Software Engineer & Desainer Manusiawi** yang taat pada prinsip arsitektur tingkat tinggi (Clean OOP, SOLID, Modular), keamanan defensif menyeluruh (Anti-Bypass, OWASP, CWE), desain human-crafted yang konsisten, dan sinkronisasi dokumentasi hidup (*Living Documentation*).

---

## 2. Masalah yang Diselesaikan (Problem Statement)

1. **AI Slop Code:** AI sering membuat kode prosedural berantakan, copy-paste berulang (*WET code*), komponen monster (>500 baris), dan mengabaikan OOP modern.
2. **Keamanan Rapuh (High-Risk Vulnerabilities):** AI kerap melupakan validasi server-side, membiarkan celah IDOR/BOLA, SQLi, menyisipkan secret ke dalam kode, atau tidak menerapkan rate-limiting.
3. **AI Slop UI/UX:** AI sering merancang antarmuka klise dengan gradien ungu neon generik, glassmorphism tak terbaca, tombol tanpa state (loading/empty/error), dan merusak design tokens yang ada.
4. **Dokumentasi Basi (Out-of-Sync Docs):** AI mengubah kode dan dependensi tanpa memperbarui `README.md`, `.env.example`, atau dokumen spesifikasi terkait.

---

## 3. Sasaran & Bukan Sasaran (Goals & Non-Goals)

### ✅ Sasaran (Goals)
- Menyediakan aturan instruksi universal (*Agent Rules*) yang kompatibel dengan semua AI tooling: Google Antigravity, Claude Code, Cursor IDE, Windsurf, GitHub Copilot, dan ChatGPT.
- Menjamin 100% kepatuhan terhadap prinsip OOP, SOLID, dan arsitektur modular yang mudah dirawat.
- Menegakkan keamanan berlapis (*Defense-in-Depth*) dari tingkat kerentanan Low hingga Critical.
- Menegakkan estetika visual yang selaras dengan design token yang telah ada dan mencerminkan craftmanship manusia.
- Menjadikan sinkronisasi dokumentasi (`README.md`, PRD, API docs) sebagai syarat mutlak penyelesaian tugas.

### ❌ Bukan Sasaran (Non-Goals)
- Menghentikan AI menggunakan kreativitas dalam pemecahan algoritma yang efisien.
- Menambah boilerplate atau layer abstraksi yang berlebihan (*overengineering*) pada proyek kecil.

---

## 4. Persona Pengguna (Target Personas)

1. **Senior Software Engineer / Tech Lead:** Ingin memanfaatkan akselerasi AI tanpa harus membuang waktu membersihkan kode sampah (*code cleanup*) dan arsitektur berantakan.
2. **Product Designer / Frontend Lead:** Ingin memastikan antarmuka yang dihasilkan AI tetap menghormati design system, responsif, aksesibel, dan bebas dari visual klise AI.
3. **Security Engineer:** Ingin kepastian bahwa setiap baris kode yang disarankan AI telah melalui filter ancaman zero-trust dan sanitasi ketat.

---

## 5. Matriks Persyaratan Fungsional (Core Requirements)

| ID | Kategori | Persyaratan Mutlak | Kriteria Keberhasilan (Acceptance Criteria) |
| :--- | :--- | :--- | :--- |
| **REQ-01** | **OOP & Reusability** | Kode harus berbasis objek bersih, mematuhi SOLID, dan reusable | Tidak ada God Class; dependensi diinjeksikan via interface/DI; komponen modular. |
| **REQ-02** | **Structure & Naming** | Struktur folder feature-based/clean architecture dengan penamaan konsisten | Nama file `kebab-case`, tidak ada file `_v2` atau `temp`, letak file terprediksi. |
| **REQ-03** | **Hardened Security** | Perlindungan penuh dari kerentanan low-high & lama-baru | Query parameterized 100%; verifikasi IDOR/BOLA di setiap endpoint; rate-limiting aktif; sanitasi input ketat; zero hardcoded secrets. |
| **REQ-04** | **Anti-Slop Design** | Desain visual selaras dengan token proyek, human-crafted | Tidak ada gradien ungu neon atau glassmorphism klise; skala 8-pt grid; 5 state UI lengkap (default, loading skeleton, empty, error, disabled). |
| **REQ-05** | **Documentation Sync** | Dokumentasi dan README wajib diperbarui bersamaan dengan perubahan kode | Setiap ada env baru, command baru, atau endpoint baru, file `README.md` dan `.env.example` langsung diupdate sebelum tugas selesai. |
| **REQ-06** | **Testing & Verification** | Verifikasi nyata sebelum menyatakan pekerjaan selesai | Kode diuji dengan test runner atau linter; tidak ada klaim sukses tanpa bukti eksekusi. |

---

## 6. Model Ancaman & Keamanan (Threat Modeling)

Setiap implementasi sistem yang dipandu oleh PRD ini harus mengevaluasi skenario ancaman berikut:
- **Spoofing Identity:** Autentikasi berbasis token dengan penandatanganan aman, CSRF protection, dan secure cookies.
- **Tampering with Data:** Validasi ketat DTO dengan schema library (Zod/Pydantic); cegah manipulasi parameter mass-assignment.
- **Repudiation:** Audit logging terstruktur tanpa membocorkan data pribadi (PII).
- **Information Disclosure:** Penyembunyian pesan error detail di production; eliminasi stack trace publik.
- **Denial of Service:** Rate-limiting di layer aplikasi dan proxy; batasan ukuran payload HTTP.
- **Elevation of Privilege:** Pengecekan otorisasi berbasis peran (RBAC) dan verifikasi kepemilikan data (anti-IDOR) pada tingkat service.

---

## 7. Roadmap & Checklist Implementasi Proyek

- [x] **Fase 1: Standar Arsitektur & Pedoman Inti**
  - [x] Pedoman OOP & Reusable Code (`guidelines/01-oop-and-reusability.md`)
  - [x] Pedoman Struktur Direktori & Konvensi Penamaan (`guidelines/02-structure-and-naming.md`)
  - [x] Pedoman Keamanan Berlapis & Anti-Bypass (`guidelines/03-hardened-security.md`)
  - [x] Pedoman Desain Anti-AI Slop (`guidelines/04-anti-ai-slop-design-system.md`)
  - [x] Pedoman Sinkronisasi Dokumentasi Hidup (`guidelines/05-documentation-and-lifecycle-sync.md`)
  - [x] Pedoman Error Handling & Pengujian (`guidelines/06-error-handling-and-testing.md`)
- [x] **Fase 2: Konfigurasi AI Agents Universal**
  - [x] Spesifikasi Universal AI Agent (`AGENTS.md`)
  - [x] Aturan untuk Claude Code (`CLAUDE.md`)
  - [x] Aturan untuk Cursor IDE (`.cursorrules`)
  - [x] Aturan untuk Google Antigravity (`.antigravity/rules/anti-slop.md`)
- [ ] **Fase 3: Adopsi Proyek & Validasi Otomatis (CI/CD Hooks)**
  - [ ] GitHub Actions linter untuk mengecek sinkronisasi README saat ada perubahan kode.
  - [ ] Git pre-commit hook untuk memvalidasi kepatuhan nama file.
