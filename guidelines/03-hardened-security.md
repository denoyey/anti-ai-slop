# 03. Hardened Security & Anti-Bypass Standard

Dokumen ini adalah **pedoman wajib keamanan tanpa kompromi**. Setiap AI coding assistant dilarang menghasilkan kode yang memiliki kerentanan keamanan, baik dengan tingkat keparahan rendah (*Low*), menengah (*Medium*), tinggi (*High*), maupun kritis (*Critical*), dari kerentanan klasik (OWASP lama) hingga teknik serangan modern (*modern API & supply chain exploits*).

---

## 1. Prinsip Utama: Zero-Trust & Defense-in-Depth

1. **Never Trust User Input (Jangan Percaya Input Klien):**
   - Validasi dan sanitasi semua input di sisi server (backend), bukan hanya di frontend.
   - Validasi tipe, format, panjang (*length*), rentang nilai (*range*), dan regex pattern.
2. **Fail Securely (Gagal dengan Aman):**
   - Jika proses autentikasi atau validasi gagal, tolak akses secara default (*deny by default*).
   - Jangan pernah mengembalikan detail stack trace, query database, atau informasi lingkungan server ke respon klien.
3. **Principle of Least Privilege (Hak Akses Minimum):**
   - Database user, container process, dan token API hanya boleh memiliki izin seminimal mungkin yang diperlukan untuk menjalankan fungsinya.

---

## 2. Matriks Penanganan Kerentanan (OWASP Top 10 & CWE)

### A. Pencegahan Injeksi (SQLi, NoSQLi, Command Injection, LDAP)
- **SQL Injection:**
  - **WAJIB:** Gunakan parameterized queries / prepared statements atau ORM yang aman.
  - ❌ **DILARANG KERAS:** Menggabungkan string secara langsung (string concatenation / template literal) ke dalam query SQL:
    ```typescript
    // DILARANG FATAL:
    db.query(`SELECT * FROM users WHERE email = '${email}'`);
    // WAJIB:
    db.query('SELECT * FROM users WHERE email = $1', [email]);
    ```
- **Command Injection:**
  - Hindari eksekusi shell command (`exec`, `eval`, `system`, `subprocess.shell=True`).
  - Jika wajib menjalankan binary, gunakan exec dengan argument array yang terisolasi dan validasi whitelist input.

### B. Broken Object Level Authorization (BOLA / IDOR)
- **IDOR (Insecure Direct Object Reference):**
  - **WAJIB:** Setiap kali user mengakses, mengubah, atau menghapus resource berdasarkan ID (misal: `/api/orders/:id`), backend **HARUS** memverifikasi apakah `order` tersebut milik user yang sedang login:
    ```typescript
    // DILARANG: Hanya mencari berdasarkan ID dari param
    const order = await orderRepo.findById(req.params.id);

    // WAJIB: Selalu scoping dengan authenticated user ID
    const order = await orderRepo.findOne({
      where: { id: req.params.id, userId: req.user.id }
    });
    if (!order) throw new NotFoundOrForbiddenException();
    ```

### C. Broken Authentication & Session Security
- **Password Hashing:**
  - Gunakan algoritma hashing modern: **Argon2id** (pilihan utama) atau **bcrypt** (cost factor minimal 12).
  - ❌ **Dilarang:** MD5, SHA1, SHA256 biasa tanpa salt/stretch.
- **JWT & Token Management:**
  - Tentukan expiry time yang singkat pada Access Token (15-60 menit).
  - Simpan Refresh Token di database untuk mendukung mekanisme pencabutan (*revocation / token blocklist*).
  - Kunci algoritma penandatanganan JWT (cegah *algorithm confusion attack* seperti `none` atau manipulasi RS256 ke HS256).
- **Cookie Security:**
  - Cookie sesi atau token auth wajib memiliki atribut: `HttpOnly`, `Secure`, `SameSite=Strict` (atau `Lax`), dan `Domain` yang valid.

### D. Cross-Site Scripting (XSS) & Content Injection
- **Output Encoding:**
  - Selalu lakukan HTML escaping pada semua data dinamis yang dirender ke browser.
  - ❌ **Dilarang:** Menggunakan `dangerouslySetInnerHTML`, `v-html`, atau `innerHTML` kecuali input sudah dibersihkan melalui library sanitizer terpercaya (seperti `DOMPurify`).
- **Content Security Policy (CSP):**
  - Pasang header CSP yang ketat: larang `unsafe-inline` dan `unsafe-eval` jika memungkinkan.

### E. Mass Assignment & Parameter Tampering
- Jangan pernah menerima payload mentah langsung ke database:
  ```typescript
  // DILARANG: Hacker bisa menyisipkan { "role": "admin", "balance": 999999 }
  await User.create(req.body);

  // WAJIB: Gunakan DTO / Schema Validator (Zod / Joi / class-validator)
  const validatedData = CreateUserSchema.parse(req.body);
  await User.create({
    name: validatedData.name,
    email: validatedData.email
    // role & balance tidak diizinkan masuk dari input bebas
  });
  ```

### F. Server-Side Request Forgery (SSRF)
- Jika aplikasi melakukan fetch HTTP ke URL dari input user (misal: webhook atau image import):
  - Validasi protokol hanya `https://`.
  - Blokir resolusi IP internal / private range: `127.0.0.1`, `localhost`, `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, dan cloud metadata `169.254.169.254`.
  - Terapkan whitelist domain tujuan jika memungkinkan.

### G. File Upload & Media Security
- Jangan mempercayai ekstensi file atau header `Content-Type` dari klien.
- Verifikasi tipe file melalui **magic bytes (file signature)**.
- Ganti nama file dengan UUID acak kriptografis (jangan simpan dengan nama asli user).
- Simpan file di luar direktori web root publik atau di Object Storage (S3 / GCS) dengan akses privat atau presigned URL bertenggat waktu.
- Batasi ukuran file maksimum (*payload limit*).

### H. Rate Limiting & DoS Mitigation
- Wajib pasang rate-limiter di endpoint sensitif:
  - `/api/auth/login` (cegah brute-force password)
  - `/api/auth/register` (cegah bot spam account)
  - `/api/auth/forgot-password` dan `/api/auth/verify-otp` (cegah OTP harvesting)
- Batasi ukuran body parser (misal: maksimal 1MB untuk JSON) guna mencegah Denial of Service via large payload.

---

## 3. Manajemen Rahasia (Secrets Management)

- ❌ **HUKUMAN MATI: Dilarang keras menaruh API Key, password DB, JWT Secret, private key di dalam kode atau commit git.**
- Selalu sediakan file `.env.example` yang hanya berisi nama variabel dan instruksi tanpa nilai rahasia.
- Validasi semua environment variables saat aplikasi start menggunakan schema (misal: `zod` atau `env-var` validator), sehingga aplikasi langsung crash saat boot jika ada secret yang hilang.

---

## 4. Security Headers Wajib (Helmet / Reverse Proxy)

Setiap respon HTTP harus dilengkapi header pengaman standar:
```http
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 0
Referrer-Policy: strict-origin-when-cross-origin
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

---

## 5. Checklist Verifikasi Keamanan Sebelum Merge Kode:

- [ ] Apakah semua input divalidasi dengan schema ketat (tipe data, format, panjang)?
- [ ] Apakah otorisasi kepemilikan resource (IDOR check) sudah diverifikasi di backend?
- [ ] Apakah query database menggunakan parameterized statement?
- [ ] Apakah endpoint sensitif sudah memiliki rate limit?
- [ ] Apakah error message menyembunyikan detail internal server (tidak membocorkan DB error / file paths)?
- [ ] Apakah tidak ada secret / credential yang tertulis langsung di kode?
