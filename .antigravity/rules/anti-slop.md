# Antigravity Rule: Anti-Slop & Enterprise Engineering Standard

Sebagai asisten Antigravity yang bekerja di repositori ini, patuhi aturan mutlak berikut:

1. **Clean OOP & Reusability:**
   - Terapkan 4 pilar OOP dan prinsip SOLID secara disiplin.
   - Pecah komponen/kelas menjadi modular dan reusable. Hindari God Class atau komponen lebih dari 300 baris.
   - Rujukan: [01-oop-and-reusability.md](file:///home/whoami/Documents/Projects/dokumentasi/guidelines/01-oop-and-reusability.md).

2. **Struktur Folder & Penamaan Konsisten:**
   - Gunakan format `kebab-case` untuk folder dan file.
   - Larang pembuatan file dengan imbuhan `_v2`, `_new`, `_backup`, `temp`.
   - Rujukan: [02-structure-and-naming.md](file:///home/whoami/Documents/Projects/dokumentasi/guidelines/02-structure-and-naming.md).

3. **Keamanan Tanpa Kompromi (Anti-Bypass & Hardened Security):**
   - Terapkan zero-trust dan sanitasi input ketat di sisi server.
   - Wajib parameterized query (anti SQLi).
   - Validasi kepemilikan resource di backend (anti IDOR/BOLA).
   - Larang hardcoded secrets, sediakan `.env.example`.
   - Rujukan: [03-hardened-security.md](file:///home/whoami/Documents/Projects/dokumentasi/guidelines/03-hardened-security.md).

4. **Desain Anti-AI Slop & Responsif Penuh (Human-Crafted UX):**
   - Hindari desain klise AI: gradien ungu neon, glassmorphism buram, ikon dekoratif acak.
   - Selalu patuhi design tokens dan skala 8-pt grid yang sudah ada.
   - Sediakan 5 state antarmuka: default, skeleton loading, empty, error, disabled.
   - Wajib 100% responsif dari 320px (iPhone SE/mini) hingga monitor 4K ultra-wide (batasi `max-w`).
   - Dukung penuh seluruh jenis iPhone: gunakan `100dvh`, patuhi Safe Area (`env(safe-area-inset-*)`), ukuran font input form minimal 16px, dan touch targets minimal 44x44pt.
   - Rujukan: [04-anti-ai-slop-design-system.md](file:///home/whoami/Documents/Projects/dokumentasi/guidelines/04-anti-ai-slop-design-system.md).

5. **Wajib Sinkronisasi Dokumentasi & README:**
   - Setiap perubahan kode yang mempengaruhi konfigurasi, endpoint, dependensi, atau arsitektur **WAJIB** langsung diperbarui di `README.md` dan dokumen terkait sebelum giliran berakhir.
   - Rujukan: [05-documentation-and-lifecycle-sync.md](file:///home/whoami/Documents/Projects/dokumentasi/guidelines/05-documentation-and-lifecycle-sync.md).

6. **Verifikasi Nyata:**
   - Selalu uji perubahan dengan runner test atau linter sebelum mengonfirmasi hasil ke pengguna.
