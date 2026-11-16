# 06. Error Handling, Logging, and Verification Standard

[English](../06-error-handling-and-testing.md) | [Bahasa Indonesia](06-error-handling-and-testing.md)

---

Dokumen ini melengkapi standar rekayasa perangkat lunak untuk memastikan kode yang dihasilkan AI tidak menyembunyikan bug (*silent failures*), memiliki penanganan error yang konsisten, dan teruji secara ketat.

---

## 1. Aturan Penanganan Error (Zero Silent Failures)

❌ **DILARANG FATAL:**
```typescript
// DILARANG: Menelan error tanpa jejak
try {
  await processPayment();
} catch (error) {
  // kosong / silent pass
}
```

### Prinsip Error Handling:
1. **Custom Domain Exceptions:**
   - Gunakan kelas error khusus turunan yang memiliki kode error semantik dan status HTTP yang jelas (misal: `EntityNotFoundException`, `UnauthorizedException`, `ValidationException`).
2. **Centralized Error Middleware:**
   - Semua error yang tidak tertangani (*unhandled errors*) harus ditangkap oleh middleware sentral di layer terluar aplikasi.
   - Di production, respon untuk error 500 harus aman: `{"status": "error", "message": "An unexpected error occurred"}` tanpa membocorkan trace atau query.
3. **Explicit Error Boundaries (Frontend):**
   - Pasang React Error Boundary pada tingkat fitur/halaman agar crash pada satu komponen tidak membuat seluruh aplikasi blank putih.

---

## 2. Standar Logging & Observability

1. **Structured Logging:**
   - Gunakan format JSON terstruktur untuk log (level: `INFO`, `WARN`, `ERROR`, timestamp, context, traceId).
2. **Perlindungan Data Sensitif (PII Redaction):**
   - ❌ **Dilarang mencatat:** password, token bearer, nomor kartu kredit, NIK, atau data rahasia lainnya ke dalam file log.
   - Selalu bersihkan objek request sebelum dicetak ke logger:
     ```typescript
     logger.info('User login attempt', { email: sanitizeEmail(user.email) });
     ```

---

## 3. Standar Pengujian & Verifikasi (Testing Standards)

Setiap kode baru harus memiliki skenario pengujian:

1. **Unit Testing:**
   - Menguji *pure logic* dan business rules secara terisolasi tanpa menyentuh database asli (gunakan mock / fake repository).
   - Uji skenario positif (*happy path*) DAN skenario negatif (*edge cases, boundary limits, invalid inputs*).
2. **Integration Testing:**
   - Uji alur antarmuka dengan database atau external adapter menggunakan container atau test database khusus.
3. **Security Testing:**
   - Uji upaya bypass autentikasi, input payload SQL injection, payload XSS, dan akses resource tanpa kepemilikan (IDOR test).
4. **Verifikasi Nyata Sebelum Mengklaim Sukses:**
   - AI wajib menjalankan runner test (`npm test`, `pytest`, `cargo test`, `go test`) atau linter/typecheck sebelum mengumumkan bahwa perbaikan selesai.
   - Jangan pernah menyatakan "fitur telah bekerja dengan sempurna" jika belum pernah diverifikasi melalui pengujian eksekusi langsung.