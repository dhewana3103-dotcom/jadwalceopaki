# CEO GTD OS — PT Raja Sukses Properindo

Dashboard backlog, jadwal, dan tracking keputusan untuk CEO. Ditenagai AI (Anthropic Claude).

## Stack

- Pure HTML + React (via CDN)
- Tailwind CSS (via CDN)
- Anthropic API (claude-sonnet-4)
- localStorage (data per browser)

## Setup & Deploy

### 1. Deploy ke Vercel
```bash
# Opsi A: via CLI
npm i -g vercel
vercel login
vercel --prod

# Opsi B: drag & drop folder ini ke vercel.com/new
```

### 2. Set API Key

Setelah app terbuka di browser:
1. Tap ⚙️ di pojok kanan atas
2. Input Anthropic API Key (`sk-ant-api03-...`)
3. Simpan

Dapatkan API key di: https://console.anthropic.com → API Keys

### 3. Bagikan URL ke tim

CEO, PA, dan PDCA masing-masing buka URL → set API key → siap pakai.

## Fitur

- **Dashboard** KPI Corporate (W1-W5) + KPI CEO 5 fungsi
- **Jadwal Harian & Mingguan** — bisa add/remove item per blok waktu
- **Dump Think** — input teks/screenshot → AI extract ke backlog
- **Backlog** — struktur Konteks + Isi + Action, assign ke PIC + deadline
- **Keputusan & Tracking** — grouped per aktivitas CEO, update tindak lanjut
- **Resume** — heatmap matrix fungsi×kategori, analisa jadwal, AI insights

## Catatan

Data disimpan di `localStorage` browser (per device). Untuk sync antar device CEO/PA/PDCA, diperlukan integrasi Supabase — lihat `DEPLOY-GUIDE.md`.

## Files

```
ceo-gtd-os/
├── index.html       ← aplikasi utama (self-contained)
├── vercel.json      ← konfigurasi Vercel
├── .gitignore
├── README.md
└── DEPLOY-GUIDE.md  ← panduan lengkap deployment & Supabase
```
