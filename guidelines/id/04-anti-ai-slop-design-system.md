# 04. Anti-AI Slop Design System & Human-Crafted UI Standard

[English](../04-anti-ai-slop-design-system.md) | [Bahasa Indonesia](04-anti-ai-slop-design-system.md)

---

Dokumen ini adalah pedoman mutlak untuk mencegah **"AI Slop"** (desain murahan, klise, generik, dan tampak seperti hasil generate bot acak). Seluruh desain antarmuka, tata letak, komponen UI, dan styling dalam proyek ini **wajib konsisten, selaras dengan design token yang ada, terasa seperti buatan desainer & software engineer manusia profesional, serta 100% responsif di seluruh spektrum perangkat (dari layar iPhone terkecil hingga monitor ultra-wide 4K)**.

---

## 1. Apa Itu "AI Slop" dalam Desain UI/UX? (HAL YANG DILARANG KERAS)

AI coding assistant sering kali memiliki bias menghasilkan desain klise yang tidak realistis. **DILARANG KERAS** memunculkan elemen-elemen berikut:

| AI Slop Anti-Pattern | Mengapa Dilarang? | Solusi Manusia Profesional |
| :--- | :--- | :--- |
| **Gradien Ungu-Biru Neon Generik** (`from-purple-600 to-blue-500` di setiap tombol/kartu) | Tampak seperti template bot crypto murahan tahun 2021 | Gunakan palet warna terkurasi dari brand system; utamakan warna solid bernuansa netral dengan aksen terukur |
| **Glassmorphism Berlebihan** (`backdrop-blur-xl bg-white/10` di semua kartu) | Tidak terbaca (*poor contrast*), merusak performa GPU, dan tidak praktis | Gunakan surface solid atau elevated card dengan border tipis dan kontras jelas (`border-border bg-card`) |
| **Floating Badges / Icon Berlingkar di Semua Tempat** | AI suka menaruh ikon dengan background lingkaran warna-warni di setiap baris teks tanpa makna | Gunakan ikon hanya jika memiliki fungsi affordance navigasi atau kategori fungsional nyata |
| **Ukuran Spacing Acak & Tidak Konsisten** (misal: margin 13px, padding 27px) | Membuat layout tampak berantakan dan amatir | **Wajib patuhi skala 8-Point Grid** (4px, 8px, 12px, 16px, 24px, 32px, 48px, 64px) |
| **Teks Placeholder Bombastis / AI Fluff** ("Unleash boundless potential with revolutionary AI synergy") | Terdengar palsu dan membingungkan pengguna | Gunakan copywriting manusia: langsung, jelas, to-the-point, dan berorientasi pada aksi nyata pengguna |
| **Mengabaikan Token Desain yang Sudah Ada** | AI menambahkan warna hex sembarangan atau mengubah font sesuka hati | **Wajib reuse CSS variables / Tailwind tokens** yang sudah didefinisikan dalam proyek |

---

## 2. Aturan Emas Keselarasan Desain (Design Consistency)

1. **Konsistensi Token (Never Break Existing Design Tokens):**
   - Periksa selalu file konfigurasi tema (`tailwind.config.js`, `theme.css`, `tokens.json`).
   - Jangan pernah menulis warna hex bebas (contoh: `#1a2b3c`) secara hardcoded di dalam komponen. Selalu gunakan semantik token (contoh: `bg-primary`, `text-muted-foreground`, `border-border`).
2. **Tipografi Berjenjang & Bertata Krama:**
   - Gunakan hierarki tipografi yang ketat:
     - **Page Title / H1:** Tegas, proporsional, line-height seimbang (tidak terlalu rapat).
     - **Section Title / H2:** Memisahkan konteks dengan jelas.
     - **Body Text:** Ukuran font minimal 14px-16px dengan `line-height: 1.5 - 1.6` untuk kenyamanan membaca.
     - **Label / Caption:** 12px-13px untuk metadata, dengan kontras yang tetap memenuhi standar WCAG AA.
3. **Ergonomi & Skala Sentuh (Touch Targets & Accessibility):**
   - Area klik/sentuh tombol minimal **44x44pt** pada perangkat layar sentuh.
   - Wajib memiliki indikator `focus-visible` (ring outline) untuk navigasi keyboard.
   - Rasio kontras teks terhadap latar belakang minimal **4.5:1** (WCAG AA).

---

## 3. Desain Harus Memiliki 5 Kondisi UI Lengkap (State Completeness)

Desain buatan manusia selalu memperhitungkan kondisi nyata aplikasi di lapangan. AI **WAJIB** membuat komponen dengan 5 state lengkap, bukan hanya state "sukses":

1. **Default / Resting State:** Tampilan normal saat data tersedia.
2. **Loading State:** Menggunakan Skeleton Loader halus yang bentuknya identik dengan konten, bukan sekadar spinner berputar di tengah layar kosong.
3. **Empty State:** Ilustrasi/ikon minimalis, pesan ramah yang menjelaskan mengapa kosong, dan tombol aksi (CTA) untuk mulai membuat data baru.
4. **Error State:** Pesan kesalahan yang jelas, manusiawi (tanpa kode error teknis), dan tombol coba lagi (*Retry*).
5. **Disabled State:** Visual transparan/redup yang jelas menandakan elemen tidak dapat diklik, dengan atribut `aria-disabled="true"`.

---

## 4. Matriks Responsif Universal (Dari HP Terkecil hingga Monitor 4K)

Antarmuka wajib teruji dan adaptif di seluruh dimensi layar nyata:

| Kategori Perangkat | Lebar Layar (Viewport) | Target Perangkat Nyata | Strategi Tata Letak |
| :--- | :--- | :--- | :--- |
| **Extra Small (HP Ringkas)** | `320px – 375px` | iPhone SE (Gen 1–3), iPhone 12/13 mini | Tata letak 1 kolom, padding kompak (`px-3`), sembunyikan aksi sekunder ke dalam menu/sheet |
| **Standard Mobile** | `390px – 430px` | iPhone 12/13/14/15/16 (Standar, Pro, Pro Max), Flagship Android | Tata letak fluid, touch targets 44pt+, navigasi bawah (*bottom bar*) |
| **Tablet Portrait** | `768px – 834px` | iPad mini, iPad 10.9", iPad Air/Pro 11" | Grid 2 kolom, split-views, elevated sheets |
| **Tablet Landscape / Laptop Kecil** | `1024px – 1280px` | iPad Pro 12.9", MacBook Air 13", Ultrabook | Sidebar navigasi collapsible, grid 3 kolom |
| **Desktop Standar** | `1440px – 1920px` | Monitor 1080p, MacBook Pro 16", iMac 24" | Dashboard multi-kolom penuh, sidebar permanen |
| **Layar 4K & Ultra-Wide** | `2560px – 3840px+` | Layar monitor 4K, 21:9 / 32:9 Ultra-Wide | **Wajib pasang batas lebar maksimal** (`max-w-7xl` / `1280px–1440px`) agar teks tidak merenggang ribuan piksel |

---

## 5. Ergonomi Khusus Ekosistem iPhone & iOS (Apple HIG Compliance)

Saat merancang tampilan web atau mobile, AI wajib mematuhi batasan khusus sistem operasi iOS:

1. **Dynamic Viewport Height (`dvh`):**
   - ❌ **DILARANG:** Menggunakan `height: 100vh` pada container layar penuh (akan tertutup oleh address bar mengambang Safari iOS).
   - ✅ **WAJIB:** Gunakan `min-h-screen min-h-dvh` atau `height: 100dvh` agar tinggi layar menyesuaikan secara dinamis saat address bar Safari mengecil atau membesar.
2. **Safe Area Insets (Notch, Dynamic Island, & Home Indicator Bar):**
   - Header fixed/sticky, bottom bar navigasi, tombol mengambang (FAB), dan modal dialog **HARUS** memperhitungkan Safe Area iOS:
     ```css
     padding-top: env(safe-area-inset-top);       /* Notch / Dynamic Island */
     padding-bottom: env(safe-area-inset-bottom); /* Home Indicator bar iPhone */
     padding-left: env(safe-area-inset-left);
     padding-right: env(safe-area-inset-right);
     ```
   - Pada proyek Tailwind CSS, gunakan kelas `pt-safe`, `pb-safe`, atau konfigurasi CSS variables `env()`.
3. **Cegah Auto-Zoom Formulir pada Safari iOS:**
   - ❌ Safari iOS akan otomatis memperbesar (*auto-zoom*) layar secara agresif jika font elemen `<input>`, `<select>`, atau `<textarea>` berukuran di bawah `16px`.
   - ✅ Semua input formulir pada tampilan mobile **WAJIB memiliki ukuran font minimal 16px** (`text-base` pada Tailwind).
4. **Touch & Momentum Scrolling Halus:**
   - Aktifkan momentum scrolling hardware-accelerated:
     ```css
     -webkit-overflow-scrolling: touch;
     overflow-y: auto;
     ```
   - Hilangkan kedipan abu-abu default saat elemen disentuh di iOS:
     ```css
     -webkit-tap-highlight-color: transparent;
     ```
5. **Standar Touch Target Apple HIG (Minimal 44x44pt):**
   - Semua elemen interaktif (tombol, ikon hamburger, tab, item menu) wajib memiliki area sentuh aktif minimal **44x44pt**, meskipun ukuran ikon grafis di dalamnya lebih kecil.

---

## 6. Checklist Verifikasi UI Sebelum Menyelesaikan Task:

- [ ] Apakah styling 100% menggunakan token/variabel desain yang ada di proyek?
- [ ] Apakah tidak ada gradien warna ungu-biru atau glassmorphism klise AI?
- [ ] Apakah semua ukuran margin dan padding mengikuti sistem kelipatan 4px / 8px?
- [ ] Apakah state Loading, Empty, dan Error sudah ditangani secara elegan?
- [ ] **Pemeriksaan Responsif Penuh:** Teruji dari 320px (iPhone SE) hingga layar 4K ultra-wide (dengan batas `max-w` yang aman)?
- [ ] **Pemeriksaan iPhone & iOS:** Menggunakan `100dvh`? Mendukung `env(safe-area-inset-*)` pada bar fixed? Input form minimal 16px? Touch target minimal 44x44pt?
- [ ] Apakah teks/copywriting terdengar alami, manusiawi, dan bebas dari kalimat klise AI?
- [ ] Apakah navigasi keyboard dan aksesibilitas kontras sudah terpenuhi?
