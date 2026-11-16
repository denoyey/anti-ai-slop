# 04. Anti-AI Slop Design System & Human-Crafted UI Standard

Dokumen ini adalah pedoman mutlak untuk mencegah **"AI Slop"** (desain murahan, klise, generik, dan tampak seperti hasil generate bot acak). Seluruh desain antarmuka, tata letak, komponen UI, dan styling dalam proyek ini **wajib konsisten, selaras dengan design token yang ada, dan terasa seperti buatan desainer & software engineer manusia profesional**.

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
     - **Label / Caption:** 12px-13px untuk metadata atau timestamp, dengan kontras yang tetap memenuhi standar WCAG AA.
3. **Ergonomi & Skala Sentuh (Touch Targets & Accessibility):**
   - Area klik/sentuh tombol minimal **44x44 piksel** pada perangkat mobile.
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

## 4. Filosofi Visual Manusiawi (Crafted & Intentional)

- **Subtlety over Loudness:** Keanggunan antarmuka modern terletak pada detail halus: border 1px bernuansa netral (`border-slate-200 dark:border-slate-800`), shadow lembut berlapis (*subtle multi-layer shadows*), dan radius sudut yang konsisten di semua komponen (misal: semua `rounded-lg` atau semua `rounded-md`).
- **Micro-Interactions yang Terasa Natural:**
  - Efek transisi halus (`transition-colors duration-150 ease-out`).
  - Animasi tidak boleh memperlambat pengguna (durasi animasi maksimal 150ms - 200ms).
- **Responsive by Design:**
  - Tidak boleh ada *horizontal scroll* yang tidak disengaja di layar smartphone.
  - Periksa tata letak tabel dan grid pada layar sempit: ubah menjadi kartu atau scrollable container yang terencana.

---

## 5. Checklist Verifikasi UI Sebelum Menyelesaikan Task:

- [ ] Apakah styling 100% menggunakan token/variabel desain yang ada di proyek?
- [ ] Apakah tidak ada gradien warna ungu-biru atau glassmorphism klise AI?
- [ ] Apakah semua ukuran margin dan padding mengikuti sistem kelipatan 4px / 8px?
- [ ] Apakah state Loading, Empty, dan Error sudah ditangani secara elegan?
- [ ] Apakah teks/copywriting terdengar alami, manusiawi, dan bebas dari kalimat klise AI?
- [ ] Apakah navigasi keyboard dan aksesibilitas kontras sudah terpenuhi?
