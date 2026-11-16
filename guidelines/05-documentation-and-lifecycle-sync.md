# 05. Living Documentation & Project Lifecycle Sync Standard

Dokumen ini menetapkan aturan mutlak: **Kode dan Dokumentasi adalah satu kesatuan yang tidak dapat dipisahkan**. AI coding assistant dilarang keras mengubah kode proyek tanpa menyelaraskan dokumentasi dan file `README.md`.

---

## 1. Aturan Wajib Sinkronisasi Dokumentasi (The Sync Rule)

Setiap kali terjadi perubahan pada proyek (penambahan fitur, refaktor, perubahan dependensi, perbaikan bug, atau konfigurasi), AI **WAJIB** mengecek dan memperbarui dokumen terkait:

### Matriks Pemicu & Dokumen yang Wajib Diperbarui:

| Jenis Perubahan Kode | Dokumen yang WAJIB Diperbarui |
| :--- | :--- |
| **Menambah / Mengubah Environment Variable** | 1. File `.env.example`<br>2. Tabel Variabel Lingkungan di `README.md` |
| **Menambah / Menghapus Dependensi Library** | 1. Instruksi instalasi di `README.md`<br>2. Alasan penambahan di PRD/Changelog |
| **Membuat Endpoint API Baru / Mengubah Payload** | 1. Spesifikasi API (OpenAPI/Swagger atau `docs/api.md`)<br>2. Bagian contoh penggunaan di `README.md` |
| **Mengubah Struktur Folder atau Arsitektur** | 1. Pohon direktori di `README.md`<br>2. Dokumen arsitektur terkait |
| **Menyelesaikan Fitur dari PRD** | 1. Checklist status di `PRD_GLOBAL.md`<br>2. Bagian Feature Matrix di `README.md` |
| **Memperbaiki Kerentanan Keamanan (Bugfix/Patch)** | 1. Catatan rilis di `CHANGELOG.md` |

---

## 2. Standar Pembaruan `README.md`

File `README.md` adalah etalase utama proyek. Pastikan `README.md` selalu mutakhir (*always up-to-date*) dengan kriteria:
1. **Langkah Instalasi & Menjalankan:** Harus akurat dan teruji. Jika ada command baru (misal: migrasi database, seeding, generate token), cantumkan urutannya secara eksplisit.
2. **Prasyarat Sistem (Prerequisites):** Versi Node.js, Python, Go, Docker, atau PostgreSQL yang didukung harus tertera jelas.
3. **Dokumentasi Variabel Lingkungan:** Setiap variabel pada `.env.example` wajib memiliki penjelasan fungsi dan contoh nilai yang aman di `README.md`.

---

## 3. Protokol Sebelum Menyatakan Tugas Selesai (Final Verification Protocol)

Sebelum AI coding assistant memberikan respon final atau menyatakan pekerjaan selesai kepada pengguna, AI wajib menjalankan checklist internal ini:

```markdown
[ ] Apakah ada file baru atau file yang dipindahkan? -> Update struktur di README.
[ ] Apakah ada env baru yang dibutuhkan? -> Tambahkan ke .env.example dan README.
[ ] Apakah ada command setup baru? -> Update panduan cara menjalankan di README.
[ ] Apakah task di PRD sudah di-centang selesai? -> Update PRD_GLOBAL.md.
[ ] Apakah dokumentasi API sudah sinkron dengan implementasi kode terbaru?
```

Jika salah satu jawaban adalah **BELUM**, AI harus memperbarui dokumentasi terlebih dahulu sebelum mengakhiri turn/tugas.

---

## 4. Standar Penulisan Riwayat Perubahan (Changelog & Commits)

Gunakan standar **Conventional Commits** untuk setiap ringkasan perubahan:
- `feat(auth): add rate limiting and argon2 password hashing`
- `fix(billing): prevent IDOR vulnerability in invoice download endpoint`
- `docs(readme): update environment variable table for OAuth setup`
- `refactor(user): decouple repository from controller using dependency injection`
- `test(security): add test suite for SQL injection prevention`
