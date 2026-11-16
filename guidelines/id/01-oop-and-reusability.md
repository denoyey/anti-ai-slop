# 01. Object-Oriented Programming (OOP) & Code Reusability Standard

[English](../01-oop-and-reusability.md) | [Bahasa Indonesia](01-oop-and-reusability.md)

---

Dokumen ini adalah aturan wajib bagi semua AI coding assistant (Antigravity, Claude, Cursor, Copilot, ChatGPT, dll.) saat merancang, menulis, dan merefaktor kode dalam repositori ini.

---

## 1. Filosofi Utama: OOP Bersih & Modular

Kode yang dihasilkan AI dilarang keras berupa *procedural spaghetti*, fungsi monolitik raksasa, atau script acak tanpa struktur objek yang jelas. Kode harus terstruktur, mudah diuji (*testable*), mudah diperluas (*extensible*), dan memiliki *domain boundary* yang tegas.

### 4 Pilar OOP Wajib:
1. **Encapsulation (Enkapsulasi):**
   - Sembunyikan *internal state*. Gunakan access modifier (`private`, `protected`) secara disiplin.
   - Jangan pernah mengekspos mutasi variabel internal secara telanjang. Gunakan metode khusus yang memvalidasi perubahan state.
2. **Abstraction (Abstraksi):**
   - Pisahkan *kontrak/antarmuka* (Interface / Abstract Class) dari *implementasi konkret*.
   - Konsumen kode harus bergantung pada kontrak antarmuka, bukan pada detail cara kerja internal.
3. **Inheritance vs. Composition:**
   - **Aturan Emas:** *Favor composition over inheritance* (Utamakan komposisi daripada pewarisan).
   - Hindari hierarki pewarisan lebih dari 2 tingkat kedalaman (`Class A -> Class B -> Class C` adalah batas maksimal).
   - Gunakan *dependency injection* dan *delegation* untuk berbagi perilaku, bukan *subclassing* yang kaku.
4. **Polymorphism (Polimorfisme):**
   - Gunakan polimorfisme untuk menghilangkan `switch-case` atau rentetan `if-else` bertingkat yang memeriksa tipe objek.
   - Manfaatkan *Strategy Pattern* atau *Factory Pattern* untuk perilaku yang dinamis.

---

## 2. Penerapan Prinsip SOLID Secara Ketat

Setiap kelas dan modul wajib mematuhi 5 prinsip SOLID:

### S – Single Responsibility Principle (SRP)
- Setiap kelas hanya boleh memiliki **satu alasan untuk berubah**.
- *Dilarang:* Membuat "God Object" / "God Class" (misal: kelas `UserManager` yang mengelola auth, query DB, mengirim email, dan merender tampilan UI).
- *Solusi:* Pecah menjadi `AuthService`, `UserRepository`, `EmailNotifier`, dan `UserPresenter`.

### O – Open/Closed Principle (OCP)
- Entitas kode harus **terbuka untuk ekstensi, tetapi tertutup untuk modifikasi**.
- Menambahkan fitur baru (misal: metode pembayaran baru, format export baru) tidak boleh mengedit kode inti yang sudah berjalan, melainkan menambahkan kelas baru yang mengimplementasikan antarmuka yang sama.

### L – Liskov Substitution Principle (LSP)
- Subtipe harus dapat menggantikan tipe induknya tanpa merusak fungsionalitas sistem.
- Jangan melempar exception `NotImplementedException` pada method turunan hanya karena kelas anak tidak membutuhkan fungsi dari kelas induk (tanda pelanggaran ISP & LSP).

### I – Interface Segregation Principle (ISP)
- Lebih baik membuat banyak antarmuka kecil yang spesifik daripada satu antarmuka gemuk (*fat interface*).
- Klien tidak boleh dipaksa untuk mengimplementasikan metode yang tidak mereka gunakan.

### D – Dependency Inversion Principle (DIP)
- Modul tingkat tinggi tidak boleh bergantung pada modul tingkat rendah; keduanya harus bergantung pada abstraksi.
- Terapkan **Dependency Injection (DI)**: Jangan melakukan instansiasi objek (`new Service()`) secara langsung di dalam kelas bisnis. Berikan instance melalui constructor injection.

---

## 3. Standar Kode Reusable (Bisa Digunakan Ulang)

Kode yang *reusable* bukan berarti kode yang over-abstracted sampai sulit dibaca. Ikuti pedoman berikut:

1. **Rule of Three (Aturan Tiga Kali):**
   - Jangan membuat abstraksi generik sebelum logika tersebut benar-benar dipakai di minimal 2 sampai 3 tempat berbeda. Hindari *premature abstraction*.
2. **Pure Functions & Stateless Utilities:**
   - Helper dan utilitas harus berupa *pure function* jika memungkinkan: input yang sama selalu menghasilkan output yang sama, tanpa *side effects* (tidak membaca/menulis state global).
3. **Data Transfer Objects (DTO) & Typed Contracts:**
   - Setiap transfer data antar layer (Controller -> Service -> Repository) harus menggunakan tipe/DTO yang tervalidasi dengan ketat, bukan payload `any`, `dict` liar, atau object tak berstruktur.
4. **Atomic Components (Untuk Frontend):**
   - Pecah UI menjadi atom terkecil: Button, Input, Modal, Typography.
   - Jangan menyatukan logic API call langsung di dalam presentational component. Pisahkan antara *Container/Smart Component* (logic & data) dan *Presentational/Dumb Component* (visual saja).

---

## 4. Design Patterns yang Dianjurkan

Gunakan pola desain standar industri berikut sesuai konteks masalah:

| Design Pattern | Kapan Digunakan | Contoh Kasus |
| :--- | :--- | :--- |
| **Repository Pattern** | Mengabstraksi layer akses data / database dari domain logic | `UserRepositoryInterface` -> `PostgresUserRepository` |
| **Strategy Pattern** | Logika algoritma/alur bervariasi berdasarkan kondisi runtime | Algoritma diskon, provider payment gateway (Midtrans, Stripe) |
| **Factory / Builder** | Pembuatan objek kompleks yang memiliki banyak parameter/langkah | Builder query, Factory pembuatan pesan notifikasi |
| **Adapter Pattern** | Menghubungkan library pihak ketiga agar tidak merusak kode inti | Pembungkus HTTP client pihak ketiga (Axios/Fetch/Guzzle) |
| **Observer / Event-Driven** | Mengirim sinyal kejadian tanpa kopling langsung (*loose coupling*) | Event `UserRegisteredEvent` ditangkap oleh `SendWelcomeEmailListener` |

---

## 5. Dilarang Keras untuk AI:

❌ **Menghasilkan file kelas lebih dari 300 baris** tanpa memecahnya menjadi modul-modul terpisah.  
❌ **Menggunakan mutable global state** (variabel global yang nilainya diubah dari berbagai tempat).  
❌ **Hardcoded business rules** di dalam presentation/UI layer.  
❌ **Duplicate code (Copy-Paste coding)** untuk logika validasi, transformasi data, dan query serupa.  
❌ **Mengabaikan typing**: Dilarang menggunakan `any`, `object`, atau type casting liar untuk membungkam linter/type checker.