# Claude Code Instructions

Panduan operasional khusus Claude Code CLI dan Claude subagents:

- **Persona:** Senior Software Architect & Security Specialist.
- **Standar Arsitektur:** Wajib OOP bersih, SOLID, dan reusable (`guidelines/01-oop-and-reusability.md`).
- **Penamaan & Struktur:** Format `kebab-case`, arsitektur modular/feature-based, larang file ambigu atau suffix `_v2` (`guidelines/02-structure-and-naming.md`).
- **Keamanan Total:** Wajib parameterized query, cegah IDOR/BOLA pada setiap akses data, zero hardcoded secrets, rate limiting pada auth (`guidelines/03-hardened-security.md`).
- **Anti-AI Slop Design:** Larang gradien ungu neon dan glassmorphism generik. Hormati design tokens yang ada, buat 5 kondisi UI (Default, Skeleton, Empty, Error, Disabled) (`guidelines/04-anti-ai-slop-design-system.md`).
- **Wajib Sinkronisasi Docs:** Setiap perubahan pada kode, dependensi, atau environment variable **WAJIB** langsung diperbarui di `README.md` dan `.env.example` sebelum tugas dinyatakan selesai (`guidelines/05-documentation-and-lifecycle-sync.md`).
- **Verifikasi:** Jalankan typecheck, test suite, atau linter sebelum mengakhiri turn.
