# 🚀 Panduan Deploy — CEO GTD OS

## Overview

App ini adalah **single HTML file** (self-contained). Bisa jalan di mana saja yang bisa serve HTML statis: Vercel, Netlify, GitHub Pages, atau bahkan dibuka langsung sebagai file lokal.

---

## Opsi 1: Deploy ke Vercel (Paling Mudah)

### Langkah-langkah

**A. Via GitHub (recommended)**

1. Buat repo baru di GitHub (bisa private)
2. Upload `ceo-gtd-os.html` dan rename jadi **`index.html`**
3. Buka [vercel.com](https://vercel.com) → Login → **Add New Project**
4. Import repo dari GitHub
5. Klik **Deploy** — selesai

URL akan jadi: `https://nama-repo.vercel.app`

**B. Via Vercel CLI**

```bash
npm i -g vercel
vercel login
# di folder berisi index.html:
vercel --prod
```

**C. Drag & drop (paling cepat)**

1. Buka [vercel.com/new](https://vercel.com/new)
2. Drag `index.html` ke zona upload
3. Deploy — selesai

---

## Opsi 2: Deploy ke Netlify

1. Buka [app.netlify.com](https://app.netlify.com)
2. Drag & drop file `index.html` ke dashboard
3. Netlify langsung deploy dan beri URL

---

## Opsi 3: GitHub Pages (Gratis, Bisa Private)

1. Buat repo di GitHub
2. Upload `index.html`
3. Settings → Pages → Source: **Deploy from branch** → `main` / `root`
4. URL: `https://username.github.io/nama-repo`

---

## Setelah Deploy — Setup API Key

Setiap orang yang pakai app harus:

1. Buka URL app
2. Tap **⚙️** di pojok kanan atas
3. Input **Anthropic API Key** (format: `sk-ant-api03-...`)
4. Klik Simpan

### Cara dapat API Key:
1. Buka [console.anthropic.com](https://console.anthropic.com)
2. Login / daftar
3. API Keys → **Create Key**
4. Copy key, paste ke settings app

> **Catatan keamanan:** API key disimpan di localStorage browser masing-masing. Tidak dikirim ke server kita, hanya ke Anthropic saat fitur AI digunakan. Gunakan 1 key tim atau 1 key per orang — keduanya oke untuk penggunaan internal.

---

## Tentang Data (localStorage)

Saat ini data disimpan di **localStorage browser** = per device, tidak sync antar device.

| Siapa | Device | Data yang terlihat |
|-------|--------|--------------------|
| CEO | HP CEO | Data CEO |
| PA | HP PA | Data PA (terpisah) |
| PDCA | Laptop | Data PDCA (terpisah) |

Ini **cukup** kalau masing-masing orang punya perannya sendiri. Masalahnya kalau CEO input dump di HP-nya, PA tidak otomatis lihat.

---

## Upgrade: Multi-Device Sync dengan Supabase

Kalau ingin CEO, PA, PDCA lihat data yang sama:

### Setup Supabase (gratis)

1. Buka [supabase.com](https://supabase.com) → New Project
2. Buat 3 tabel:

```sql
-- Tabel backlog
create table backlog (
  id text primary key,
  data jsonb not null,
  updated_at timestamp default now()
);

-- Tabel keputusan
create table keputusan (
  id text primary key,
  data jsonb not null,
  updated_at timestamp default now()
);

-- Tabel jadwal
create table jadwal (
  tanggal text primary key,
  data jsonb not null,
  updated_at timestamp default now()
);
```

3. Aktifkan **Row Level Security** → buat policy: semua bisa read/write (internal tool)
4. Copy **Project URL** dan **Anon Key** dari Settings → API

### Integrasi ke app

Di file `index.html`, cari bagian ini di App component:

```javascript
// Ganti fungsi ld() dan sv() dengan Supabase client
```

Tambahkan Supabase JS CDN di `<head>`:
```html
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
```

Ganti localStorage dengan Supabase calls. Atau hubungi tim teknis untuk implementasi — estimasi 2-3 jam pekerjaan.

---

## Biaya Estimasi

| Platform | Biaya |
|----------|-------|
| Vercel (hosting) | **Gratis** (Hobby plan) |
| Netlify (hosting) | **Gratis** (Free plan) |
| GitHub Pages | **Gratis** |
| Supabase (database) | **Gratis** sampai 500MB, 2 project |
| Anthropic API | ~$0.003/request · misal 100 dump/bulan ≈ **$0.30/bulan** |

Total estimasi: **< $1/bulan** untuk penggunaan tim kecil (CEO + PA + PDCA).

---

## Troubleshooting

**AI tidak jalan setelah deploy?**
→ Pastikan API key sudah diset di ⚙️ Settings

**"API key belum diset" terus padahal sudah input?**
→ Coba clear cache browser, atau cek apakah browser allow localStorage (mode incognito biasanya tidak)

**Mau restrict akses hanya untuk tim?**
→ Di Vercel: Settings → **Password Protection** (Vercel Pro, $20/bulan)
→ Alternatif gratis: Cloudflare Access (deploy ke Cloudflare Pages)

---

*Generated for CEO GTD OS · PT Raja Sukses Properindo*
