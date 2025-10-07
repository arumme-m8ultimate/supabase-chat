# Supabase Chat Sederhana

Aplikasi chat real-time berbasis [Supabase](https://supabase.com), sangat ringan, bisa langsung dideploy di GitHub Pages tanpa backend tambahan.

---

## ✨ Fitur

- **Realtime chat:** pesan langsung muncul tanpa refresh.
- **Input nama user:** nama disimpan di browser (tidak perlu login/email).
- **UI minimalis:** mudah dikembangkan untuk fitur lain.
- **Gratis deploy:** hanya butuh akun Supabase dan GitHub.

---

## 🚀 Cara Deploy di GitHub Pages

1. **Fork atau clone repo ini** ke akun GitHub kamu.
2. **Edit file `index.html`:**
   - Ganti `SUPABASE_URL` dan `SUPABASE_ANON_KEY` (lihat di dashboard Supabase > Project Settings > API).
3. **Aktifkan GitHub Pages:**
   - Masuk ke repo → **Settings** → **Pages**
   - Source: pilih `main` dan folder `/ (root)`
   - Klik **Save**
4. **Akses aplikasi:**  
   `https://USERNAME.github.io/supabase-chat/`

---

## 🛠️ Setup Database di Supabase

### 1. **Buat Table `messages`**
```sql
create table public.messages (
  id uuid primary key default gen_random_uuid(),
  sender_name text not null,
  content text not null,
  created_at timestamp with time zone default now()
);
```

### 2. **Aktifkan RLS (Row Level Security)**
Aktifkan di menu Table Editor > messages > Enable RLS.

### 3. **Tambah Policy agar semua bisa kirim & baca pesan**
```sql
-- Bisa SELECT (baca)
create policy "Anyone can read messages" on messages
  for select
  using (true);

-- Bisa INSERT (kirim)
create policy "Anyone can send messages" on messages
  for insert
  with check (true);
```

---

## 📦 Struktur File

```
supabase-chat/
├── index.html      # UI utama chat (langsung konek ke Supabase)
└── README.md       # Dokumentasi & petunjuk deploy
```

---

## 💬 Contoh Penggunaan

1. Buka aplikasi di browser.
2. Isi nama pada kolom "Nama".
3. Tulis pesan dan klik "Kirim".
4. Pesan akan muncul real-time untuk semua user.

---

## 🔒 Catatan Keamanan

- **JANGAN** masukkan `SERVICE ROLE KEY` ke file HTML (hanya pakai ANON KEY).
- Semua data chat bersifat publik (siapa saja bisa baca & kirim pesan).
- Untuk login/fitur privat, kembangkan lebih lanjut dengan Auth Supabase.

---

## ❤️ Kontribusi

- Pull request, issue, dan saran sangat diterima!
- Silakan fork, modifikasi, dan kembangkan untuk kebutuhanmu.

---

## 📄 Lisensi

MIT

---

> Dibuat dengan ❤️ menggunakan [Supabase](https://supabase.com) dan GitHub Pages.
